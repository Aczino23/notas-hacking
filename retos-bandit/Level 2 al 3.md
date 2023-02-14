## Objetivo:
The password for the next level is stored in a file called **spaces in this filename** located in the home directory.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
-  **Port:** 2220
- **User:** bandit2 
- **Password:** rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

## Solución:

``` bash
bandit2@bandit:~$ ls
spaces in this filename
bandit2@bandit:~$ cat ./spaces\ in\ this\ filename
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
bandit2@bandit:~$
```

## Notas adicionales:
El comando de Linux **cat** concatena archivos y los muestra en el salida estándar.

## Referencias:
-[Google Search for “spaces in filename”](https://www.google.com/search?q=spaces+in+filename)
