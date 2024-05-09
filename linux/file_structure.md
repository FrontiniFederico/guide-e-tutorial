## File structure

La documentazione ufficiale la trovi direttamente da cli con `man hier` ma è molto dettagliata. Riporto qui le parti più basiche che sicuramente serve sapere.

- `/root` è la home dir dell'utente root.
- `/home` qui dentro trovi le home dir degli utenti normali.
- `/bin` contiene gli eseguibili. `/sbin` è lo stesso ma per gli utenti di servizio.
- `/etc` contiene file di configurazione.
- `/var` contiene file la cui dimensione è variabile nel tempo. Molto importante è la subdir `/var/log` che contiene appunto i file di logging.

