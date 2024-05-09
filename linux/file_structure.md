## File structure

La documentazione ufficiale la trovi direttamente da cli con `man hier` ma è molto dettagliata. Riporto qui le parti più basiche che sicuramente serve sapere.

- `/root` è la home dir dell'utente root.
- `/home` qui dentro trovi le home dir degli utenti normali.
- `/bin` contiene gli eseguibili. `/sbin` è lo stesso ma per gli utenti di servizio.
- `/etc` contiene file di configurazione.
- `/var` contiene file la cui dimensione è variabile nel tempo. Molto importante è la subdir `/var/log` che contiene appunto i file di logging.

## Cheat sheet basico

| Path          | Description                                |
|---------------|--------------------------------------------|
| /             | The Root Directory                         |
| /bin          | Essential User Binaries                    |
| /boot         | Static Boot Files                          |
| /cdrom        | Historical Mount Point for CD-ROMs         |
| /dev          | Device Files                               |
| /etc          | Configuration Files                        |
| /home         | Home Folders                               |
| /lib          | Essential Shared Libraries                 |
| /lost+found   | Recovered Files                            |
| /media        | Removable Media                            |
| /mnt          | Temporary Mount Points                     |
| /opt          | Optional Packages                          |
| /proc         | Kernel & Process Files                     |
| /root         | Root Home Directory                        |
| /run          | Application State Files                    |
| /sbin         | System Administration Binaries             |
| /selinux      | SELinux Virtual File System                |
| /srv          | Service Data                               |
| /tmp          | Temporary Files                            |
| /usr          | User Binaries & Read-Only Data             |
| /var          | Variable Data Files                        |
