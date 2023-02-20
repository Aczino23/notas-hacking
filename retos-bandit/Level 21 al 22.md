## Objetivo:
A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit21
- **Password:** NvEJF7oVjkddltPSrdKEFOllh9V1IBcq

## Solución:
Vemos el contenido del directorio `/etc/cron.d/`:

```bash
bandit21@bandit:~$ ls /etc/cron.d
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24       e2scrub_all  sysstat
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root  otw-tmp-dir
bandit21@bandit:~$
```

Como estamos buscando la password del reto 22, vemos el archivo `cronjob_bandit22`:

```bash
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@bandit:/etc/cron.d$
```

Analizando lo que ejecuta este cron:

-   `@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null`: después de un reinicio, ejecuta `/usr/bin/cronjob_bandit22.sh &> /dev/null` como el usuario `bandit22`
-   `* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null`: cada minuto ejecuta `/usr/bin/cronjob_bandit22.sh &> /dev/null` como el usuario `bandit22`

Revisamos el script `cronjob_bandit22.sh`:

```bash
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit21@bandit:/etc/cron.d$
```

Ahora sabemos que este pasa la password de `bandit22` al archivo `t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv` almacenado en `/tmp/`, y le da permisos `644`, indicando que cualquiera puede leerlo:

```bash
bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff
bandit21@bandit:/etc/cron.d$
```

## Notas adicionales:
- Cron es un **administrador de tareas de Linux que permite ejecutar comandos en un momento determinado,** por ejemplo, cada minuto, día, semana o mes. Si queremos trabajar con cron, podemos hacerlo a través del comando crontab.

- Cron se ejecutará cada minuto comprobando los ficheros _`/var/spool/cron`_ o **`/`**_`etc/crontab.`_

Estas herramientas utilizan una serie de comandos básicos, como por ejemplo:

-   **_`contrab archivo`_**: funciona para reemplazar el archivo contrab con uno nuevo.
-   **_`contrab -e`_**: edita la entrada del archivo contrab.
-   **_`contrab –l`_**: su función es obtener un listado con todas las tareas del archivo.
-   **_`contrab -r:`_** borra el archivo contrab de forma permanente.
-   **_`contrab -c dir`_**: indica dónde se almacenará el archivo. Para utilizar este comando, se requiere de ciertos permisos de ejecución.
-   **_`contrab -u usuarios`_**: funciona para gestionar el contrab de otros usuarios.

Además de estos comandos, Linux cuenta con una serie de **cadenas de texto que vienen preconfiguradas** para programar scripts automáticamente, siendo las más comunes:

-   `**@reboot**`, el cual ejecuta el script una vez se inicie el equipo.
-   `**@yearly**` **o `@anually`**, que funciona para ejecutar el script una vez al año.
-   `**@monthly**` ejecuta una vez al mes el script, el primer día de cada mes.
-   `**@weekly**`, el cual ejecuta el script una vez a la semana.
-   `**@daily**`, que funciona para ejecutar una vez al día el script.
-   `**@midnight**`, el cual ejecuta el script todas las noches a las 00:00 horas.
-   `**@hourly**` ejecuta el script durante el primer minuto de cada hora.
- 
## Referencias:
- https://keepcoding.io/blog/como-usar-cron-y-crontab-en-linux/
