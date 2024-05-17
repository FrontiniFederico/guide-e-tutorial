## Configurazione chiave ssh

Utilizziamo una chiave ssh per connettersi in modo sicuro a un server di cui abbiamo le credenziali. Dalla macchina da cui vogliamo entrare in ssh eseguiamo i seguenti comandi:
- `ssh-keygen -t rsa -b 4096 -f ~/.ssh/<nome_chiave>`
- `ssh-copy-id -i ~/.ssh/<nome_chiave>.pub <utente>@<ip_server>`

Ora possiamo entrare nel server remoto con il comando `ssh -i ~/.ssh/<nome_chiave> <utente>@<ip_server>`. Lungo e scomodo, potremmo voler modificare `~/.ssh/config` e aggiungere il seguente:

```conf

# ...

Host <hostname_del_server>
    HostName <ip_server>
    User <utente>
    IdentityFile ~/.ssh/<nome_chiave>
```

Ora possiamo accedere più agilmente con il comando `ssh <hostname_del_server>`. 

Se lo vogliamo fare a mano o siamo partiti da una coppia di chiavi già presenti sul server:

1. Nel server, ssicuriamoci che la chiave pubblica sia copiata dentro `~/.ssh/authorized_keys`.
2. Copiamo la chiave privata dal server in `~/.ssh/` nel client.
3. L'utenza deve avere permessi esclusivi verso la chiave privata:
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/*
```