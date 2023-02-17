## Objetivo:
The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!).

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit12
- **Password:** JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

## Solución:
Revisamos el archivo `data.txt`, y vemos que posee información hexadecimal:

```bash
bandit12@bandit:~$ cat data.txt
00000000: 1f8b 0808 8e0b bf63 0203 6461 7461 322e  .......c..data2.
00000010: 6269 6e00 013c 02c3 fd42 5a68 3931 4159  bin..<...BZh91AY
00000020: 2653 598c b471 f700 0014 ffff fa59 c6c5  &SY..q.......Y..
00000030: af63 cfff af73 ffff bdb7 7c9f b1fb eafa  .c...s....|.....
00000040: bfff fb9f f9fe bdbf ffeb ffef b001 3b2c  ..............;,
00000050: 5900 0341 a064 007a 8003 40d0 6869 a068  Y..A.d.z..@.hi.h
00000060: 3464 007a 81a0 0680 3401 90d0 6800 00d1  4d.z....4...h...
00000070: a0c9 a680 f51e 9a83 27a4 3d4f 4991 0000  ........'.=OI...
00000080: 69a6 803d 4001 9001 a686 8c40 0d00 d3d2  i..=@......@....
00000090: 0d00 0d06 08f5 0323 4034 069e a340 0da8  .......#@4...@..
...
```

Siguiendo las instrucciones, creamos la carpeta en el directorio `/tmp`, y copiamos el archivo:

```bash
bandit12@bandit:~$ mkdir /tmp/wf1
bandit12@bandit:~$ cp data.txt /tmp/wf1/.
bandit12@bandit:~$ cd /tmp/wf1
bandit12@bandit:/tmp/wf1$ ls
data.txt
bandit12@bandit:/tmp/wf1$
```

Para pasar el hexdump a un archivo `normal`, usamos el comando `xxd`. Este tiene la opción `-r`, que permite convertir un hexdump a un binario. Al convertir el archivo, vemos que este se encuentra comprimido con `gzip`:

```bash
bandit12@bandit:/tmp/wf1$ xxd -r data.txt data
bandit12@bandit:/tmp/wf1$ file data
data: gzip compressed data, was "data2.bin", last modified: Wed Jan 11 19:18:38 2023, max compression, from Unix, original size modulo 2^32 572
bandit12@bandit:/tmp/wf1$
```

Por lo tanto, le cambiamos el nombre al archivo para que quede con la extensión `gz` (de gzip), y lo descomprimimos con la opción `-d` del comando:

```bash
bandit12@bandit:/tmp/wf1$ mv data data.gz
bandit12@bandit:/tmp/wf1$ gzip -d data.gz
bandit12@bandit:/tmp/wf1$ ls
data  data.txt
bandit12@bandit:/tmp/wf1$ file data
data: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/wf1$
```

Una vez más, vemos que este se encuentra comprimido; pero esta vez, en formato `bzip2`. Ahora, cambiamos el nombre al archivo con la extensión `bz2`, y lo descomprimimos con la opción `-d`:

```bash
bandit12@bandit:/tmp/wf1$ mv data data.bz2
bandit12@bandit:/tmp/wf1$ ls
data.bz2  data.txt
bandit12@bandit:/tmp/wf1$ bzip2 -d data.bz2
bandit12@bandit:/tmp/wf1$ file data
data: gzip compressed data, was "data4.bin", last modified: Wed Jan 11 19:18:38 2023, max compression, from Unix, original size modulo 2^32 20480
bandit12@bandit:/tmp/wf1$
```

Una vez más el archivo se encuentra comprimido con `gzip`, por lo tanto, lo volvemos a descomprimir:

```bash
bandit12@bandit:/tmp/wf1$ mv data data.gz
bandit12@bandit:/tmp/wf1$ ls
data.gz  data.txt
bandit12@bandit:/tmp/wf1$ gzip -d data.gz
bandit12@bandit:/tmp/wf1$ file data
data: POSIX tar archive (GNU)
bandit12@bandit:/tmp/wf1$
```

Esta vez, el archivo se encuentra comprimido en `tar`, el cual, descomprimimos con las opciones `x` (extraer), `v` (verbose) y `f` (indica el archivo):

```bash
bandit12@bandit:/tmp/wf1$ mv data data.tar
bandit12@bandit:/tmp/wf1$ ls
data.tar  data.txt
bandit12@bandit:/tmp/wf1$ tar xvf data.tar
data5.bin
bandit12@bandit:/tmp/wf1$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/wf1$
```

Otra vez, este se encuentra en `tar`:

```bash
bandit12@bandit:/tmp/wf1$ mv data5.bin data.tar
bandit12@bandit:/tmp/wf1$ ls
data.tar  data.txt
bandit12@bandit:/tmp/wf1$ tar xvf data.tar
data6.bin
bandit12@bandit:/tmp/wf1$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/wf1$
```

Ahora descomprimimos el archivo `bzip2`:

```bash
bandit12@bandit:/tmp/wf1$ mv data6.bin data.bz2
bandit12@bandit:/tmp/wf1$ ls
data.bz2  data.tar  data.txt
bandit12@bandit:/tmp/wf1$ bzip2 -d data.bz2
bandit12@bandit:/tmp/wf1$ file data
data: POSIX tar archive (GNU)
bandit12@bandit:/tmp/wf1$
```

Una vez más en `tar`:

```bash
bandit12@bandit:/tmp/wf1$ mv data data.tar
bandit12@bandit:/tmp/wf1$ ls
data.tar  data.txt
bandit12@bandit:/tmp/wf1$ tar xvf data.tar
data8.bin
bandit12@bandit:/tmp/wf1$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Wed Jan 11 19:18:38 2023, max compression, from Unix, original size modulo 2^32 49
bandit12@bandit:/tmp/wf1$
```

Y por último, descomprimimos el archivo `gzip` para obtener el archivo de texto con la password:

```bash
bandit12@bandit:/tmp/wf1$ mv data8.bin data.gz
bandit12@bandit:/tmp/wf1$ gzip -d data.gz
bandit12@bandit:/tmp/wf1$ file data
data: ASCII text
bandit12@bandit:/tmp/wf1$ cat data
The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
bandit12@bandit:/tmp/wf1$
```

## Notas adicionales:

| Comando | Descripción |
| --- | --- |
| mkdir | Esta herramienta es usada para crear un nuevo subdirectorio o carpeta del sistema de archivos. El nombre **mkdir** tiene su origen en las palabras _**make subdirectory**_ que significan: crear subdirectorio en inglés. |
| xxd | Crea un volcado hexadecimal de un archivo. También puede convertir un volcado hexadecimal de nuevo a su forma binaria inicial. Además, puede ser utilizado para realizar parches archivo binario
| xxd -r | -r transforma de hexadecimal a binario.|
| gzip | es una utilidad de la línea de comandos que nos permite crear y extraer archivos `.gz` |
| bzip2 | El comando de linux bzip2 se utiliza para comprimir archivos. Cada archivo se sustituye por una versión comprimida de sí mismo con extensión .bz2. |
| tar | El **comando TAR** es usado para comprimir o empaquetar un archivo o directorio. |
| mv | para mover archivos y directorios de un directorio a otro o para renombrar un archivo o directorio. |

## Referencias:
- [Hex dump on Wikipedia](https://en.wikipedia.org/wiki/Hex_dump)
- https://denovatoanovato.net/comando-mkdir/