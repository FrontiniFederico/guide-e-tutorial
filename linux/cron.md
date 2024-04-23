## cron

Ci permette di fare *task scheduling*. Ogni user nel sistema ha il suo set di *cronjobs*. L'insieme di cronjobs per un utente è chiamato *crontab*:
- `crontab -l` vedi i cronjobs per l'utente
- `crontab -e` editi la lista di cronjobs con l'editor scelto. La prima volta te lo fa scegliere da quelli disponibili, altrimenti devi usare il comando `select editor` o manualmente con `EDITOR=nano crontab -e`. Nota che non andiamo a editare direttamente il crontab, ma ci fa modificare un file temporaneo che se va bene viene installato. 

Un cronjob ha sei campi: `* * * * * <comando>`. I primi cinque campi sono nella forma:

| Campo         | Descrizione                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------|
| Minuto        | Valore compreso tra 0 e 59. Indica il minuto in cui il comando verrà eseguito.               |
| Ora           | Valore compreso tra 0 e 23. Indica l'ora in cui il comando verrà eseguito.                   |
| Giorno mese   | Valore compreso tra 1 e 31. Indica il giorno del mese in cui il comando verrà eseguito.      |
| Mese          | Valore compreso tra 1 e 12. Indica il mese in cui il comando verrà eseguito.                 |
| Giorno settimana | Valore compreso tra 0 e 7 (0 e 7 rappresentano Domenica). Indica il giorno della settimana in cui il comando verrà eseguito. (1 = Lunedì, 2 = Martedì, ..., 7 = Domenica) |

Ad esempio: `* 8 * * 1 echo "hello world"`: ogni lunedì mattina alle 8 stampa "hello world".

Volendo, i primi cinque comandi possono essere sostituiti con `@<frequenza>`, dove le opzioni sono:
- `@hourly`
- `@daily` o `@midnight`
- `@weekly`
- `@monthly`
- `@yearly` o `@annually`
- `@reboot`

Non è consigliato eseuguire il cronjob con il tuo utente. Magari abbiamo un utente di automazione o lo facciamo da root. Possiamo farlo con l'opzione `-u`:
- `crontab -u automator -e`. Se vuoi usare `root` ovviamente devi precedere con `sudo` ed essere fra i sudoers. 

Nota bene che se vogliamo eseguire uno script con un cronjob faremmo meglio a inserire il path completo dello script o dell'eseguibile anche se il prefisso è nel `$PATH`. Questo perché l'utente che lo esegue potrebbe non averlo nel `$PATH` e comunque dipende dalla distro. 

Se sei pigro, [crontab-generator](https://crontab-generator.org) ti fa il cronjob.