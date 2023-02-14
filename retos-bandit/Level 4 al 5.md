## Objetivo:
The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit4 
- **Password:** 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

## Solución:

```bash
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls
-file00  -file02  -file04  -file06  -file08
-file01  -file03  -file05  -file07  -file09
bandit4@bandit:~/inhere$ file ./-file0*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
bandit4@bandit:~/inhere$
```

## Notas adicionales:
El comando **``file``** sirve para determinar el tipo de archivo.

Con este comando podemos comprobar fácilmente el tipo de fichero, esto es útil porque no tiene extensión, que por algún motivo creemos no es la correcta o porque desconfiamos por alguna razón. Y entre otras cosas muestra la codificación de caracteres de los archivos de texto, srt, etc.

## Referencias:
- https://travesuras.wordpress.com/2013/02/28/20130228-1/


