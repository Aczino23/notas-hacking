## Objetivo:
A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE:** Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit22
- **Password:** WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff

## Solución:
Vemos el contenido del directorio `/etc/cron.d/`, y revisemos que se encuentra ejecutando el archivo `cronjob_bandit23`:

```bash
bandit22@bandit:~$ cd /etc/cron.d
bandit22@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24       e2scrub_all  sysstat
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root  otw-tmp-dir
bandit22@bandit:/etc/cron.d$
```

Este se encuentra ejecutando el script `cronjob_bandit23.sh` que se encuentra en el directorio `/usr/bin/`:

```bash
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:/etc/cron.d$
```

```bash
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit22@bandit:/etc/cron.d$
```

Lo que hace este script es:

-   Asigna a la variable `myname` el valor de la salida del comando `whoami`, que en este caso es _bandit22_
-   Luego, asigna a la variable `mytarget` el siguiente output:
    -   Toma el resultado de `echo I am user $myname` (_I am user bandit22_), y lo manda a `md5sum`
    -   Este entrega el hash MD5 del mensaje anterior (`169b67bd894ddbb4412f91573b38db3 -`). Y por último, esto es entregado al comando `cut -d ' ' -f1`
    -   El último comando separa el mensaje MD5 usando el delimitador de un espacio `' '`, y muestra el primer campo de esto, que es `169b67bd894ddbb4412f91573b38db3`

El problema al ejecutar el script anterior, es que el resultado está basado en bandit22, por lo tanto, debemos hacerlo de la siguiente forma para obtener la password de _bandit23_:

```bash
bandit22@bandit:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G
bandit22@bandit:/etc/cron.d$
```

## Notas adicionales:
- En su forma más básica, un shell-script puede ser un simple fichero de texto que contenga uno o varios comandos. Para ayudar a la identificación del contenido a partir del nombre del archivo, es habitual que los shell scripts tengan la extensión «.sh», por lo que seguiremos este criterio (pero recuerde que es algo meramente informativo y opcional).
- 
## Referencias:
- http://trajano.us.es/~fjfj/shell/doc/shellscript2.html
- https://bioinf.comav.upv.es/courses/unix/scripts_bash.html