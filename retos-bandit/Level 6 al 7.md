## Objetivo:
The password for the next level is stored **somewhere on the server** and has all of the following properties:

-   owned by user bandit7
-   owned by group bandit6
-   33 bytes in size

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit6
- **Password:** P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

## Solución:
Con el comando **``find``** podemos buscar archivos dentro del sistema. Conocemos la opción **``-size``**, que permite buscar por el peso del archivo. Ahora vemos en el manual, las opciones para buscar por el propietario (usuario), con la opción **``-user``**, y que la opción **``-group``** nos permite buscar por el grupo al que se encuentra asociado:

Y como no sabemos en qué carpeta del sistema se encuentra, lo buscamos desde la raíz de este (**``/``**):

```bash
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c
find: ‘/dev/mqueue’: Permission denied
find: ‘/dev/shm’: Permission denied
find: ‘/var/spool/bandit24’: Permission denied
find: ‘/var/spool/rsyslog’: Permission denied
find: ‘/var/spool/cron/crontabs’: Permission denied
...
bandit6@bandit:~$
```

El problema que se presenta en la imagen, corresponden a múltiples errores de **``Permission denied``**, los cuales, pertenecen a STDERR (standard error). Cuando se ejecuta un proceso y se produce un error, los mensajes que se muestran en consola son standard errors (como en este caso, donde no tenemos permisos para ver algunos directorios).

El STDERR es identificado con el número **``2``**, y sus mensajes pueden ser redirigidos (usando el símbolo `>`) a **``/dev/null``** (archivo especial utilizado para descartar información):

```bash
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$
```

Ahora que encontramos el archivo con esas características, podemos leerlo sin problemas:

```bash
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
bandit6@bandit:~$
```

## Notas adicionales:
1. Linux te brinda la opción de buscar archivos según sus tamaños. La sintaxis básica para buscar archivos por tamaño es:

```bash
find <startingdirectory> -size <size-magnitude> <size-unit>
```

Puedes especificar las siguientes unidades de tamaño:

-   **c** – bytes
-   **k** – kilobytes
-   **M** – megabytes
-   **G** – gigabytes
-   **b** – trozos de 512 bytes

2. Linux te da la capacidad de especificar tus búsquedas según la propiedad del archivo. Para buscar archivos de un determinado propietario, se debe ejecutar el siguiente comando:

```bash
find / -user john
```

3. Esto devolverá una lista de todos los archivos que posee el usuario llamado **john**. Similar a los nombres de usuario, también podemos buscar archivos a través de nombres de grupo:

```bash
find / -group classroom
```

## Referencias:

- https://www.hostinger.mx/tutoriales/como-usar-comando-find-locate-en-linux/
- https://atareao.es/tutorial/terminal/redirigir-entrada-y-salida-en-linux/