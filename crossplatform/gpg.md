# Aggiungere una chiave gpg a git

`gpg`sta per GNU Privacy Guard ed è una suite crittografica per lo scambio sicuro di messaggi. Ne generiamo una da usare su git per avere i commit firmati. L'unico prerequisito è avere verificato la mail su git. Una guida più verbosa in inglese è nei [docs di GitHub](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key). Puoi consultare anche [questo video](https://www.youtube.com/watch?v=xj9OiJL56pM&t) passo passo, sempre in inglese e che prende come esempio Windows.

Dal terminale, eseguire i seguenti passaggi:
1. `gpg --full-generate-key`, poi segui il prompt. Fai una chiave RSA a 4096 cifre per garantire la massima sicurezza e inserisci i tuoi dati. Quando ti chiede la mail, assicurati sia quella verificata su git. 
2. Con `gpg --list-secret-keys --keyid-format=long` controlla la tua chiave, dovrebbe essere nel formato:
```shell
$ gpg --list-secret-keys --keyid-format=long
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
uid                          Hubot <hubot@example.com>
ssb   4096R/4BB6D45482678BE3 2016-03-10
```
3. Copia l'id della chiave, nell'esempio è `3AA5C34371567BD2`.
4. Copia la chiave pubblica, che puoi ottenere lanciando il comando `gpg --armor --export <id_chiave>`. Sarà nella forma:
```shell
-----BEGIN PGP PUBLIC KEY BLOCK-----
# blabla
-----END PGP PUBLIC KEY BLOCK-----
```

Sul tuo GitHub, clicca su `Settings/SSH and GPG keys/New GPG Key` e aggiungi la chiave pubblica, dandole un nome riconoscibile. Torna sul terminale e completa la procedura. 
```
git config --global user.name "YOUR-NAME"
git config --global user.email "YOUR-EMAIL"
git config --global user.signingkey YOUR-KEY-ID 
git config --global commit.gpgsign true
git config --global tag.gpgsign true
git config --global gpg.program "/usr/bin/gpg"
```

## Aggiungere una chiave ssh a git

Se non hai una coppia di chiavi pubbliche e private sulla tua macchina, leggi il [tutorial dedicato](ssh.md). Una volta che hai una coppia di chiavi, possiamo aggiungerle a git:

1. Facciamo partire l'ssh-agent in background: `eval "$(ssh-agent -s)"`
2. Aggiungiamo la chiave privata: `ssh-add ~/.ssh/<nome_chiave>`
3. Ora copiamo il contenuto della chiave pubblica. Andiamo su GitHub e clicca su `Settings/SSH and GPG keys/New SSH Key`. Copia il contenuto della chiave pubblica.