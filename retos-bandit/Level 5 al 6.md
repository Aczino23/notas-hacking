## Objetivo:
The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:

-   human-readable
-   1033 bytes in size
-   not executable

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit5 
- **Password:** lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

## Solución:

Ingresamos al directorio **inhere** y mostramos el contenido del directorio con el comando **``ls -l``** 

``` bash
bandit5@bandit:~/inhere$
bandit5@bandit:~/inhere$ cd
bandit5@bandit:~$
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls -l
total 80
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere00
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere01
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere02
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere03
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere04
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere05
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere06
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere07
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere08
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere09
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere10
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere11
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere12
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere13
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere14
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere15
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere16
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere17
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere18
drwxr-x--- 2 root bandit5 4096 Jan 11 19:19 maybehere19
bandit5@bandit:~/inhere$
```

Con el comando **``find``** buscamos el archivo cuyo tamaño sea de 1033 bytes y que dicho archivo no sea un archivo ejecutable y que sea legible por humanos:

```bash
bandit5@bandit:~/inhere$ find -size 1033c -exec file {} + | grep ASCII
./maybehere07/.file2: ASCII text, with very long lines (1000)
bandit5@bandit:~/inhere$
```

Mostramos el contenido del archivo .file2 el cual se encuentra dentro del directorio maybehere07:

```bash
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```

## Notas adicionales:
El comando **find** es el comando que más se utiliza para encontrar y filtrar archivos en Linux. El diseño básico de este comando es el siguiente:

```bash
find <startingdirectory> <options> <search term>
```

El argumento **startingdirectory** es el punto de origen de donde deseas iniciar la búsqueda. Puede ser reemplazado con varios argumento, incluyendo:

-  **/ (slash)**  – busca en todo el sistema. 
-   **. (punto)**  – busca en la carpeta en la que estás trabajando actualmente (directorio actual).
-   **~ (tilde)**  – para buscar desde tu directorio home.

Linux te brinda la opción de buscar archivos según sus tamaños. La sintaxis básica para buscar archivos por tamaño es:

```bash
find <startingdirectory> -size <size-magnitude> <size-unit>
```

Puedes especificar las siguientes unidades de tamaño:

-   **c** – bytes
-   **k** – kilobytes
-   **M** – megabytes
-   **G** – gigabytes
-   **b** – trozos de 512 bytes

## Referencias:

- https://www.hostinger.mx/tutoriales/como-usar-comando-find-locate-en-linux/