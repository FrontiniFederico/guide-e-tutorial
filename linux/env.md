## lavorare con variabili d'ambiente e locali

Si dividono in due sottocategorie:
- locali, disponibili sono nel processo corrente all'interno della shell e non ereditate dai suoi sottoprocessi. 
- variabili d'ambiente, disponibili nella sessione corrente e in tutti i sottoprocessi da essa generati. Possono essere globali o specifiche dell'utente. 

Per creare una variabile locale, ad esempio, `saluto`, basta fare `saluto=ciao`. Posso ispezionare il contenuto della variabile:
```
echo $saluto
# ciao
# se ora apro una nuova shell e riprovo non ottengo nulla
```
Posso eliminare la variabile locale con `unset saluto`.

per creare una variabile d'ambiente devo usare `export`. Posso esportare la variabile appena create: `export saluto` o esportare una nuova variabile direttamente con `export ringraziamento=grazie`. 

Per elencare le variabili posso usare:
- `set`. Mostra sia le variabili locali che quelle d'ambiente
- `printenv`. Elenca solo le variabili d'ambiente.

Le variabili d'ambiente esportate in questo modo valgono solo per la sessione corrente. Se le vogliamo rendere persistenti dobbiamo inserirla in qualche file di configurazione.

Innanzitutto, le variabili d'ambiente possono avere diversa visibilità. Si dividono in:
- globali
- utente

A seconda della loro visibilità, potremmo volerle aggiungere in uno di questi file di configurazione:

### A livello di sistema

- `/etc/environment`: specificamente destinato alle variabili d'ambiente
- `/etc/env.d/*`: variabili d'ambiente, suddivise in più file
- `/etc/profile`: tutti i tipi di script di inizializzazione
- `/etc/profile.d/*`: script di inizializzazione
- `/etc/bashrc`, `/etc/bash.bashrc`: destinati a funzioni e alias

### Specifico per l'utente

- `~/.profile`: usato per tutte le shell
- `~/.pam_environment`: parte dei moduli di autenticazione pluggabili per Linux
- `~/.bash_profile`: inizializzazione per le shell di login (bash)
- `~/.bashrc`: inizializzazione per tutte le shell interattive (bash)
- `~/.cshrc`, `~/.zshrc`, `~/.tcshrc`: simile per shell non bash

È sconsigliato modfiicare direttamente in `/etc/profile`, la cosa più semplice è customizzare le variabili presente all'avvio con scriptini anche banali in `/etc/profile.d/`.