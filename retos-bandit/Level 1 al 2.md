## Objetivo:
The password for the next level is stored in a file called **-** located in the home directory

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit1 
- **Password:** NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

## Solución:
```bash
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
bandit1@bandit:~$
```

## Notas adicionales:
El comando **cat** no puede mostrar el contenido del archivo ya que el nombre de dicho archivo es un carácter especial por lo cual lo que se debe hacer es realizar una cat al archivo pero especificando la ruta completa del archivo.

## Referencias:
-   [Google Search for “dashed filename”](https://www.google.com/search?q=dashed+filename)
-   [Advanced Bash-scripting Guide - Chapter 3 - Special Characters](http://tldp.org/LDP/abs/html/special-chars.html)