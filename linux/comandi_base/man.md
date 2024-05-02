## Informazioni sui comandi 

Per reperire informazioni sui comandi che abbiamo a disposizione in linux e il loro funzionamento abbiamo a disposizione il comando `man nome_comando`. Stampa a schermo la pagina del manuale del comando in questione, con le varie opzioni e argomenti. Ad esempio, se lancio `man pwd`:

```cli
PWD(1)                                              User Commands                                              PWD(1)

NAME
       pwd - print name of current/working directory

SYNOPSIS
       pwd [OPTION]...

DESCRIPTION
       Print the full filename of the current working directory.

       -L, --logical
              use PWD from environment, even if it contains symlinks

       -P, --physical
              avoid all symlinks

       --help display this help and exit

       --version
              output version information and exit

       If no option is specified, -P is assumed.

       NOTE: your shell may have its own version of pwd, which usually supersedes the version described here.  Please
       refer to your shell's documentation for details about the options it supports.
```

Per comandi più complessi, la pagina del manuale rischia di essere dispersiva. Per questo è molto utile il comando `tldr` che ne fornisce una versione condensata. Possiamo installarlo facilmente (l'esempio per *Ubuntu*):

```
sudo apt install tldr
tldr - u
```

Se a questo punto lanciamo `tldr pwd` otteniamo il seguente:

```
pwd
Print name of current/working directory.More information: https://www.gnu.org/software/coreutils/pwd.

 - Print the current directory:
   pwd

 - Print the current directory, and resolve all symlinks (i.e. show the "physical" path):
   pwd -P
```

E se non conosciamo il nome del comando ma abbiamo una idea di cosa fa? Possiamo cercarlo usando, indifferentemente, `man -k <keyword>` o `apropos <keyword>`:

```
federico@FROFED-NB-DELL:~$ apropos "working directory"
chdir (2)            - change working directory
fchdir (2)           - change working directory
get_current_dir_name (3) - get current working directory
getcwd (2)           - get current working directory
getcwd (3)           - get current working directory
getwd (3)            - get current working directory
git-stash (1)        - Stash the changes in a dirty working directory away
pwd (1)              - print name of current/working directory
pwdx (1)             - report current working directory of a process
cd (n)               - Change working directory
pwd (n)              - Return the absolute path of the current working directory
Tcl_Chdir (3)        - manipulate the current working directory
Tcl_GetCwd (3)       - manipulate the current working directory
```

Alcuni comandi non hanno una pagina del manuale. Tipicamente questo avviene perché sono comandi della shell. Se stiamo usando `bash`, possiamo usare il comando `help <comando_builtin>` per recuperare informazioni a riguardo:

```
federico@FROFED-NB-DELL:~$ help export
export: export [-fn] [name[=value] ...] or export -p
    Set export attribute for shell variables.

    Marks each NAME for automatic export to the environment of subsequently
    executed commands.  If VALUE is supplied, assign VALUE before exporting.

    Options:
      -f        refer to shell functions
      -n        remove the export property from each NAME
      -p        display a list of all exported variables and functions

    An argument of `--' disables further option processing.

    Exit Status:
    Returns success unless an invalid option is given or NAME is invalid.
```

E può darsi che anche se il comando non ha una sua pagina del manuale abbia lo stesso qualche informazione in `tldr`:

```
federico@FROFED-NB-DELL:~$ tldr export
export
Export shell variables to child processes.More information: https://manned.org/export.1posix.

 - Set an environment variable:
   export {{VARIABLE}}={{value}}

 - Append a pathname to the environment variable PATH:
   export PATH=$PATH:{{path/to/append}}
```
Per verificare se il comando che stiamo cercano è builtin nella shell usiamo il comando `type`:

```
federico@FROFED-NB-DELL:~$ type export
export is a shell builtin
federico@FROFED-NB-DELL:~$ type man
man is hashed (/usr/bin/man)
federico@FROFED-NB-DELL:~$ type tldr
tldr is hashed (/usr/bin/tldr)
federico@FROFED-NB-DELL:~$
```

Se vuoi informazioni più approfondite, il comando `info` lancia un documento ipertestuale che contiene un indice navigabile per cercare le informazioni che ti servono.