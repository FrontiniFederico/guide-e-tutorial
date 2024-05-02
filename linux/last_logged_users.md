## Verificare login 

Per verificare quanti utenti sono attivi, quali sono inattivi, quando fanno il login e per quanto tempo rimangono collegati puoi usare la tripletta di comandi `last`, `lastb` e `lastlog`.

### last

Prende le informazioni da `/var/log/wtmp` e ci fa vedere gli ultimi login divisi per utente e per quanto tempo sono rimasti collegati:
- `last -n <int>` o direttamente `last -<int>` mostra gli *n* login più recenti. È equivalente a `last | head -<int>`.
- `last -aF` mostra la data per esteso e sposta l'hostname alla fine per evitare troncamenti.
- `last <utente>` mostra gli ultimi login dell'utente indicato. Puoi indicare più utenti separandoli con uno spazio.
  - `last reboot` e `last shutdown` in particolare mostrano le attività dello pseudouser indicato.
- `last <terminal>` puoi filtrare per tipologia di terminale come `pts` o `tty`.
- `last -d` per mostrare l'username e non l'ip. Per togliere direttamente l'ip/hostname usiamo `-R`
- `last -p <orario>` per mostrare chi è connesso adesso (con `now`) o all'orario specificato.

### lasb

Mostra gli ultimi login falliti, recuperati in `/var/log/btmp`. Richiede permessi elevati.

### lastlog

Mostra gli ultimi login effettuati da tutti gli utenti nel server. Utile per capire chi non si collega da tanto ed eventualmente togliere l'utenza. Attento che diversi account di servizio non si collegano a una shell perché come specificato in `/sbin/nologin` non possono farlo.
- `lastlog -u <utente>` per vedere l'ultimo login di un utente specifico.
- `lastlog -b <giorni>` per vedere login più vecchi di *n* giorni.
- `lastlog -t <giorni>` per vedere login più recenti di *n* giorni.