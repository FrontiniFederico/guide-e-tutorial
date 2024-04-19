## Pacman

- Refreshare la cache che contiene info sulle versioni dei pacchetti disponibili: `sudo pacman -Syy`
- Installare un pacchetto: `sudo pacman -S htop`
- Rimuovere un pacchetto: `sudo pacman -R htop`

E se non ne so il nome? 

- `pacman -Ss pygame`

Ti restituisce una lista di risultati correlati. Pacman ti installa automaticamente le dipendenze di ogni pacchetto che installi. Posso anche 

- installare più pacchetti insieme, basta separarli con uno spazio: `sudo pacman -S htop tmax python-pygame`
- rimuovere gli *orphans*, cioè pacchetti che non usa più nessuno, posso cercarli con `pacman -Qdt`
- fare un *system upgrade*, posso farlo con `sudo pacman -Syu`

Mai aspettare più di un mese per farlo, arch ha bisogno di update costanti. Un buon middle ground è due settimane.

### Update i mirror list

Potrei volerlo fare perché un `sudo pacman -Syy` ci mette tanto. Potrebbe voler dire che il primo server da cui prendo i pacchetti non è più disponibile. In ogni caso, è buona norma rigenerare il mirror list all’incirca ogni mese. 

- Leggi la [documentazione sui mirror](https://wiki.archlinux.org/title/mirrors) nell’archlinux wiki.
- Vai alla pagina [Pacman Mirrorlist Generator](https://archlinux.org/mirrorlist/) e genera il mirror per l’Italia. Copia le prime righe, non ci servono tutti. I primi 20 o 30 bastano.
- Nella macchina, vai in `/etc/pacman.d`
- Fai un `ls` per vedere i file disponibili. Dovresti avere un file a nome `mirrorlist`
- Crea un backup: `sudo cp /etc/mirrorlist /etc/mirrorlist.bak`
- Svuotiamo il file mirrorlist: `sudo truncate -s 0 mirrorlist`
- Copiamo il contenuto dal website all’interno del file mirrorlist ora vuota e decommenta i primi tre quattro server, qualcuno per l’Italia e magari un paio francesi o austriaci.
- Sincronizziamo: `sudo pacman -Syy`