## usermod

- Aggiungere un utente a un gruppo: `sudo usermod -aG <gruppo> <utente>` Chiaramente posso fare questa operazione solo se l'utente che esegue il comando è nei sudoers. Se non lo è, un sudoer o root può aggiungerlo con `(sudo) usermod -aG sudo <utente>`. Presta attenzione che a seconda della distro il gruppo dei sudoers potrebbe non chiamarsi *sudo* ma qualcos'altro. Puoi aggiungere l'utente a più gruppi, basta separarli con una virgola e.g. `sudo usermod -aG admins, sudo fed`. Nota che devi fare *logout* e *login* per vedere in essere i cambiamenti apportati.
- Cambiare la *home directory*: `sudo usermod -d /home/<nome> (--move-home) <utente>`. Se la directory non esiste, il comando la crea. L'argomento `--move-home` sposta i contenuti della vecchia home in quella nuova. Nota che non si può fare se ad eseguire l'operazione è l'utente target. 
- Cambiare nome: `sudo usermod -l <nome_nuovo> <nome_vecchio>`. Puoi verificare che il cambiamento è avvenuto dando un occhio, ad esempio, a `/etc/passwd`.
- Bloccare un utente: `usermod -L <nome>`
- Sbloccare un utente: `usermod -U <nome>`
- Impostare la scadenza della password: `usermod <nome> -e YYYY-MM-DD`. Verfica il cambiamento avvenuto con `chage -l <nome>`.

## groupadd 

- Creare un nuovo gruppo: `sudo groupadd <gruppo>`.

## groups 

- Verficare a che gruppi appartiene l'utente: `groups <utente>`.

## adduser

- Creare un nuovo utente: `sudo adduser <nome_utente>`