## Objetivo:
The password for the next level is stored in a hidden file in the **inhere** directory.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit3 
- **Password:** aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

## Solución:

```bash
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Jan 11 19:19 .
drwxr-xr-x 3 root    root    4096 Jan 11 19:19 ..
-rw-r----- 1 bandit4 bandit3   33 Jan 11 19:19 .hidden
bandit3@bandit:~/inhere$ cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
bandit3@bandit:~/inhere$
```

## Notas adicionales:
El comando **`ls -l`** para listar el contenido del directorio en un formato de tabla con columnas incluidas:
-   permisos de contenido.
-   número de enlaces al contenido.
-   propietario del contenido.
-   propietario del grupo del contenido.
-   tamaño del contenido en bytes.
-   fecha / hora de la última modificación del contenido.
-   nombre de archivo o directorio.

El comando `ls -a` para listar archivos o directorios, incluidos archivos o directorios ocultos. En Linux, cualquier cosa que comience con un **`.`** se considera un archivo oculto.

## Referencias: