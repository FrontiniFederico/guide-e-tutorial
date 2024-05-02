## sudo

Il comando `sudo` ci permette di eseguire comandi con i privilegi di root senza generare una nuova shell. L'accesso a `sudo` non è abilitato di default, ma possiamo usarlo quando il nostro utente è fra i sudoer e ha bisogno di permessi elevati per fare qualcosa. Ad esempio, se sono loggato come utente normale e provo a eseguire `apt update` vedo dei messaggi di errore:

```
Reading package lists... Done
E: Could not open lock file /var/lib/apt/lists/lock - open (13: Permission denied)
E: Unable to lock directory /var/lib/apt/lists/
W: Problem unlinking the file /var/cache/apt/pkgcache.bin - RemoveCaches (13: Permission denied)
W: Problem unlinking the file /var/cache/apt/srcpkgcache.bin - RemoveCaches (13: Permission denied)
```

Per passare a root posso:
- Elevare la mia shell o aprirne una nuova con i seguenti comandi: `sudo -i`, `sudo -s` o `su -`. Hanno delle leggere differenze:
  - `sudo -i` lancia una nuova login shell per l'utente root loggato nella sua home directory. È simile a fare il login direttamente come root. È il più potente.
  - `sudo -s` lancia una nuova shell, ma non una nuova login shell. Non cambia l'ambiente. Praticamente i comandi li fa un superuser ma l'ambiente rimane quello dell'utente che ha lanciato il comando di sudo. 
  - `su -` equivalente a `sudo -i`. Posso usare `su -p` per renderlo simile a `sudo -s` (*p* sta per `--preserve-environment`).

Non è opportuno lasciare abilitata l'utenza root, tantomeno il login in ssh diretto quindi diamo a un utente i privilegi di root. Lo vorremmo aggiungere al gruppo dei sudoer, ma il nome di questo gruppo cambia in base alla distro. Scopriamo come si chiama nella nostra macchina: `sudo cat /etc/sudoers`. Sbagliare la sintassi di questo file può rompere il sistema quindi il file va modificato non tramite editor ma con il comando `visudo` che apre un editor con validazione della sintassi. Verso la fine del file, leggiamo:

```
# User privilege specification
root    ALL=(ALL:ALL) ALL
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```

Cosa significa la sintassi di questa riga? 
- <mark>root</mark>    ALL=(ALL:ALL) ALL il nome dell'utente a cui la regola si riferisce.
- root    <mark>ALL</mark>=(ALL:ALL) ALL a quali host si applica la regole (ha senso se è un cluster)
- root    ALL=(<mark>ALL</mark>:ALL) ALL quali utenti può impersonare l'utente
- root    ALL=(ALL:<mark>ALL</mark>) ALL quali gruppi può impersonare l'utente
- root    ALL=(ALL:ALL) <mark>ALL</mark> che comandi l'utente può usare con privilegi elevati

Ad esempio, se vogliamo permettere a un utente di automazione chiamato `automator` di gestire gli aggiornamenti del server possiamo farlo così:

`automator ALL=(ALL:ALL) /usr/bin/apt`

Possiamo fare in modo che la regola lasci fare i comandi elevati all'utente senza chiedere la password. Da usare con cautela, perché è un rischio di sicurezza. Per farlo:

`automator ALL=(ALL:ALL) NOPASSWD: /usr/bin/apt`

La sintassi per i gruppi è la stessa, ma `%` indica che si parla di un gruppo e non di un utente. Il file termina con questa riga che sembra un commento ma non lo è:

```
#includedir /etc/sudoers.d
```

Questa riga specifica che i file ogni file nella directory indicata che non inizi per `#` o per `.` veranno letti, validati e aggiunti alla configurazione di `sudo`. Alcune applicazioni all'installazione applicano modifiche ai privilegi di root e avere le loro modifiche in un unico file lì dentro rende più semplice intervenire e sapere chi aggiunge quali utenti e permessi. Per editare uno di questi file, uso `sudo visudo -f /etc/sudoers.d/<file_to_edit>`


Ora sappiamo il nome del gruppo, nel caso di Ubuntu *sudo*. Verifichiamo se l'utente appartiene al gruppo sudo con `groups <utente>`:

```
groups <utente>
<utente> : <utente> adm dialout cdrom floppy sudo audio dip video plugdev netdev
```

Per modificare l'appartenenza a un gruppo leggi [qui](usermod.md).

- `sudo -l` per vedere che permessi elevati ho come utente.
- `sudo !!` per lanciare il precedente comando con sudo. Utile se dimentico il prefisso `sudo` di un comando molto lungo.

Se faccio un errore di sintassi maneggiando `/etc/sudoers` con `visudo`, ottengo qualcosa di simile:

```
>>> /etc/sudoers: syntach error near line 21 <<<
What now?
```
`visudo` purtroppo non ti dice che opzioni hai, ecco cosa puoi fare:
- `e` per editare il file e sperabilmente correggere l'errore.
- `x` per uscire dal file senza salvare i cambiamenti errati che hai appena tentato di apportare.
- `q` per salvare comunque i cambiamenti invalidi. Da non usare.