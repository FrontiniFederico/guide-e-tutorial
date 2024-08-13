## Sequenza di Boot

- Bios (16 bit):
  - Esegue il POST Power On Self Test che controlla lo stato della memoria.
  - Carica lo STAGE 1 Boot Loader dal MBR, ossia i primi 512 byte del disco designato per il boot.
  - Carica lo STAGE 2 Boot loader
  - Carica l'OS