# less

Il comando `less` apre un file in letturas interattiva. Permette di fare avanti e indietro nel file e di cercare all'interno del documento.

## cat vs more vs less

Tutti e tre questi comandi sembrano fare la stessa cosa, in linea di principio. In realtà ci sono alcune differenze fondamentali:
- `cat` dumpa il contenuto del file nello `stdout`. Il suo scopo principale infatti è più quello di concatenare e appendere file.
- `more` permette di scrollare avanti e indietro.
- `less` fa quello che fa `more` ma aggiunge funzionalità. Non carica tutto il file in memoria ma pagine alla volta, permette di inserire segnalibri nel testo e cercare occorrenze.

In sostanza, `cat` è preferibile se si devono fare operazioni con più file. Per vedere semplicemente un log o un file è meglio `less`.

## Utilizzo

- `less <filename>` per aprire il file.
- `/` per cercare dall'inizio alla fine. `n` per cercare il successivo verso il basso e `N` per il precedente verso l'alto.
- `?` per cercare dalla fine all'inizio. `n` per cercare il successivo verso l'alto e `N` per il precedente verso il basso.
  - Se devi cercare un URL o un `path` ti conviene usare la ricerca all'indietro per non dovere usare i caratteri di escape: `? /path/to/file` al posto di `/ \/path\/to\/file`.
- Puoi simulare un `tail -f` premendo `F` direttamente dentro `less`.
- Puoi mettere bookmarks e tornare in posizioni salvate nella sessione corrente. Premi `m` e poi `<lettera>` per salvare il segnalibro. Per tornare alla posizione di un segnalibro: `' <lettera>`.

### Cheat sheet

| Shortcut   | Description                      |
|------------|----------------------------------|
| CTRL+F     | Forward one window               |
| CTRL+B     | Backward one window              |
| CTRL+D     | Forward half window              |
| CTRL+U     | Backward half window             |
| j          | Navigate forward by one line     |
| k          | Navigate backward by one line    |
| G          | Go to the end of the file        |
| g          | Go to the start of the file      |
| q          | Exit the less pager              |
| v        | Using the configured editor, edit the current file |
| h        | Summary of less commands                      |
| &pattern | Display only the matching lines, not all     |
