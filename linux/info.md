## Comandi utili sullo stato generale del server

- `lsb_release -a` per informazioni generali (`-a` sta per *all*). Da lanciare con `sudo`.
- `cat /etc/os-release` stampa i contenuti del file indicato a schermo. Su Neteye uso questo, di solito.
- `uname -a` stampa informazioni di sistema (`-a` sta per *all*).
- `uptime` da quanto la macchina è in piedi.
- `whoami`, `who`,`w` per sapere lo username con cui stai loggato, chi è loggato e cosa sta facendo rispettivamente.

## Informazioni hardware

- `lshw`, informazioni dettagliate sulla configurazione hardware. Stampa una sfilza di informazioni, ha più senso filtrarle con `grep`.
- `lscpu`, `lsblk`, `lspci`, `lsusb` per informazioni su cpu, block devices, pci e usb rispettivamente.

## Monitoraggio 

- `free -h` per sapere quanta RAM stai usando.
- `vmstat` per informazioni sulla memoria virtuale.
- `htop` per una scheda interattiva sui processi in esecuzione e il loro peso.
- `df -h`, `du -h` per info sullo spazio disco e le dimensioni delle cartelle.
- `ifconfig` o `ip address` per informazioni sul networking. Attenzione che non dà informazioni sul consumo di rete.
- `netstat -a` per informazioni sulla rete, compreso il consumo. Per un controllo continuo usa `ifstat` (esci con *CTRL+C*).
- `sudo iftop -e <interfaccia=eth0>` per informazioni dettagliate sul traffico. 
