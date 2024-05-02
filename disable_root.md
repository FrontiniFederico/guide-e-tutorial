## Disabilitare accesso come root in ssh

L'utente di root ha tutti i privilegi nel server. Di default, facciamo il login e agiamo come superuser ma è una pratica sconsigliata. È molto meglio come misura di sicurezza avere un utente fra i sudoers che può elevarsi a utente root e con gli stessi privilegi e disabilitare l'accesso in ssh come root. 

Se il nostro server è aperto possiamo notare che sta venendo attaccato costantemente da bot che cercano di accedere. Accediamo al server come root o con un utente che ha i privilegi da sudoer, meglio la seconda visto che disabiliteremo l'accesso come root. Se facciamo `sudo cat /var/log/auth.log` otteniamo qualcosa di simile:

```
May  2 06:49:20 ubuntu-frofed sshd[89922]: Failed password for invalid user admin from 85.209.11.254 port 7788 ssh2                                                                                                     May  2 06:49:21 ubuntu-frofed sshd[89922]: Connection closed by invalid user admin 85.209.11.254 port 7788 [preauth]                                                                                                    May  2 06:49:23 ubuntu-frofed sshd[89924]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=61.177.172.181  user=root                                                            May  2 06:49:24 ubuntu-frofed sshd[89924]: Failed password for root from 61.177.172.181 port 57694 ssh2     May  2 06:49:30 ubuntu-frofed sshd[89924]: message repeated 2 times: [ Failed password for root from 61.177.172.181 port 57694 ssh2]                                                                                    May  2 06:49:32 ubuntu-frofed sshd[89924]: Received disconnect from 61.177.172.181 port 57694:11:  [preauth]May  2 06:49:32 ubuntu-frofed sshd[89924]: Disconnected from authenticating user root 61.177.172.181 port 57694 [preauth]                                                                                               May  2 06:49:32 ubuntu-frofed sshd[89924]: PAM 2 more authentication failures; logname= uid=0 euid=0 tty=ssh ruser= rhost=61.177.172.181  user=root                                                                     May  2 06:50:14 ubuntu-frofed sshd[89926]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=61.177.172.181  user=root                                                            May  2 06:50:16 ubuntu-frofed sshd[89926]: Failed password for root from 61.177.172.181 port 45849 ssh2     May  2 06:50:24 ubuntu-frofed sshd[89926]: message repeated 2 times: [ Failed password for root from 61.177.172.181 port 45849 ssh2]  
```

Scopriamo che il nostro server ha ricevuto molte richieste di autenticazione da agenti che non riconosciamo. Se la nostra password è sicura non abbiamo problemi ma possiamo proteggerci disabilitando l'accesso come root. Lanciamo `sudo nano /etc/ssh/sshd_config` o con l'editor che preferiamo. 

```
# ...roba

#LoginGraceTime 2m
PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

# ...roba
```

Modifichiamo `PermitRootLogin` da *yes* a *no*, salviamo e usciamo dall'editor. Le modifiche apportate non hanno effetto finché non rebootiamo il servizio: `sudo systemctl restart sshd`. Se adesso provi a fare login come utente root direttamente vedrai qualcosa di simile: 

```
ssh root@46.101.199.86
root@46.101.199.86's password:
Permission denied, please try again.
```
