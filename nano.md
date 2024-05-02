## nano

È un editor di testo semplice e adatto a chi si approccia per la prima volta a linux. Prima di usarlo, assicuriamoci che sia installato: `which nano` che ci dice dove si trova il binary del comando. Diverse distro lo installano di default, in caso un banale `sudo apt install nano` (per Ubuntu) lo installa. Ci muoviamo nell'editor con le frecce. In fondo troviamo funzionalità a cui si accede premendo `ctrl+<lettera>`. Ad esempio, `^O Write Out` ci dice che premendo `ctrl+o` possiamo salvare il file.

- `nano` senza specificare un file apre un editor vuoto. 
- `nano <path_to_file>` per aprire un file specifico. Se apri un file per cui non hai i permessi di scrittura, nano ti apre il file in modalità sola lettura e te lo dice. 

Alcuni comandi utili:
- `ctrl+w` per cercare testo nel file. Nota che quando lo fai i comandi disponibili cambiano. Posso ad esempio andare ad una specifica linea con `^T`. Una volta trovato il testo, premere ancora `^W` ti manda al prossimo match.
- `ctrl+k` per tagliare l'intera linea e `ctrl+u` per incollare. 
- `ctrl+g` per aprire una guida.
- `nano + <numero> <path_to_file` per aprire l'editor alla linea specifica. Utile se apro uno script o un playbook perché magari so dove si è piantato o qualcosa del genere.
- `nano -v <path_to_file>` per aprire un file in sola lettura.