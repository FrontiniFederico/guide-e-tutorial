# Midnight Commander

Midnight Commander è un file manager crossplatform e molto leggero per agevolere la navigazione del file system laddove la command line potrebbe risultare scomoda e una GUI lenta.

### Comandi di navigazione

Nel documento, `C` sta per `Ctrl` e `A` sta per `Alt`.

| Shortcut | Direzione | Significato   |
|----------|-----------|---------------|
| ^+F       | Destra    | "Forward"     |
| ^+B       | Sinistra  | "Backwards"   |
| ^+N       | Giù       | "Next"        |
| ^+P       | Su        | "Previous"    |

- Se il command prompt è abilitato, posso usare il command prompt per navigare il file system: `cd /path/to/...`. Se non lo è, posso usare `A+C`.
- `^+S` per cercare all'interno del pannello. Se il command prompt è disabilitato, posso scrivere direttamente.
- Per selezionare più file, `shift` e freccia. Per deselezionare, `shift` e ripassaci sopra.
  - Premi `+` per fare una regex al posto di selezionarli a mano.

### Modificare il file system

- Per cancellare un file `F8`. Chiederà conferma.
- Puoi copiare un file con `F5` e muovere con `F6`. Copiare o Muovere un file esegue il comando nell'altro pannello. Per aprire la directory di destinazione nell'altro pannello posso:
  - Cambiare pannello e spostarmi a mano.
  - `A+I` fa un sync dei pannelli. Il pannello a sinistra diventa anche il pannello a destra.
  - `A+O` per aprire la dir selezionata nell'altro pannello.
- `mc` ha un editor di testo a cui puoi accedere con `F4`. Entri in sola lettura con `F3`. Posso disabilitare quello di default, in questo caso `mc` ti fa usare quello di sistema. Per farlo vai in `Options/Configuration`.
- `F2` per accedere al menu. Posso da qui comprimere una cartella.
  - di default non mi farebbe comprimere in un file `zip`, ma per farlo posso:
    1. Apro il menu con `F2`.
    2. Uso `@ Do something on the current file`
    3. Mi apre un command prompt. Scrivo: `zip <nome file>.zip`.

### Collegarsi in ssh 

- Devi configurare l'accesso alla macchina come descritto nella [guida dedicata](https://github.com/FrontiniFederico/guide-e-tutorial/blob/main/linux/ssh.md).
- Ti colleghi andando su `Right/Shell link` e indicando l'hostname. Ti apre la macchina target nel pannello dove eri posizionato.
- Muovere e copiare file avviene esattamente come indicato alla precedente sezione. 

## Cheat Sheet

preso da [qui](https://gist.github.com/samiraguiar/9cd4264445545cfd459d).

### Main View

- File/directory operations

| Shortcut    | Description                                          |
|-------------|------------------------------------------------------|
| F3          | View file                                            |
| Shift + F3  | View raw file (disregard extension)                  |
| F5          | Copy selected files                                  |
| F6          | Move selected files                                  |
| Shift + F6  | Rename file under cursor                             |
| Shift-F4    | Create a new file                                    |
| C-x d       | Compare directories                                  |
| C-x c       | Chmod dialog                                         |
| C-x o       | Chown dialog                                         |
| C-x C-s     | Edit symlink                                         |
| C-x s       | Create symlink dialog                                |
| C-x l       | Create hard link dialog                              |
| C-x v       | Run relative symbolic link tool on selected or tagged items |
| C-x a       | List active VFS directories                          |


- Selection

| Shortcut    | Description                                       |
|-------------|---------------------------------------------------|
| Insert / C-t | Select/deselect file                              |
| *           | Invert selection on files                         |
| +           | Specify file selection options (including custom pattern) |
| -           | Same as above, but for deselecting                |


- Navigation

| Shortcut          | Description                                                              |
|-------------------|--------------------------------------------------------------------------|
| TAB /  / C-i      | Jump from one panel to the other                                         |
| F9                | Select the top menu bar                                                  |
| Esc Esc           | Quickly dismiss menus/pop-ups (skip the timeout for "Single press" from the configuration) |
| A-c               | Quick cd dialog                                                          |
| A-?               | Search dialog                                                            |
| C-s               | Search for item                                                          |
| A-s               | Incremental search (A-s again to jump to next occurrence)                |
| A-y               | Move to the previous directory in the directory history                  |
| A-u               | Move to the next directory in the directory history                      |
| A-Shift-h         | Show path history                                                        |
| C-\               | Directory Hotlist                                                        |
| C-p / Up arrow    | Move selection bar to the previous entry in the panel                    |
| C-n / Down arrow  | Move selection bar to the next entry in the panel                        |
| A-g               | Move selection bar to the first visible item in the panel                |
| A-r               | Move selection bar to the middle item in the panel                       |
| A-j               | Move selection bar to the last visible item in the panel                 |
| A-v / Page up     | Move selection bar one page up                                           |
| A-p / Page down   | Move selection bar one page down                                         |
| A-< / Home        | Move selection bar to the top (first entry)                              |
| A-> / End         | Move selection bar to the bottom (last entry)                            |


- Display

| Shortcut    | Description                                                              |
|-------------|--------------------------------------------------------------------------|
| C-r         | Refresh current panel                                                    |
| C-u         | Swap panels                                                              |
| A-,         | Toggle panel layout (horizontal/vertical)                                |
| C-x i       | Toggle other panel to information mode                                   |
| C-x q       | Toggle other panel to quick view mode                                    |
| A-i         | Make the other panel show the same directory as the current               |
| A-o         | Display the contents of the highlighted directory in the other panel      |
| A-t         | Change panel view (full, brief, long)                                    |
| A-.         | Toggle "Show Hidden Files" feature                                        |


- Command prompt

| Shortcut        | Description                                                              |
|-----------------|--------------------------------------------------------------------------|
| C-o             | Drop to the console                                                      |
| A-Enter         | Put the name of the highlighted file on the command line                 |
| C-x t           | Put the name of the selected items on the command line                   |
| C-Shift-Enter   | Put the full path of the highlighted file on the command line            |
| A-a / C-x p     | Put the full path of the pane directory on the command line              |
| A-h             | Show command history                                                     |
| A-n / A-p       | Navigate up/down through the command history                             |
| C-x !           | External Panelize (fill current panel with the output of a command)      |
| C-x j           | Show background jobs                                                     |
| F2-@            | Run a command on the currently highlighted item, e.g.:                   |
|                 |   - F2-@ unzip                      : Unzip selected file              |
|                 |   - F2-@ zip -r foo.zip             : Zip current directory as foo.zip |
|                 |   - F2-@ 7za x                      : Extract selected file with 7zip |
|                 |   - F2-@ 7za a foo.7z               : 7zip current directory as foo.7z  |


- Others

| Shortcut     | Description                                 |
|--------------|---------------------------------------------|
| Shift-F10    | Quiet exit, without confirmation            |



### File View

| Shortcut | Description            |
|----------|------------------------|
| C-f      | View the next file     |
| C-b      | View the previous file |
