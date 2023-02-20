## Objetivo:
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit19
- **Password:** awhqfNnAbc1naukrpqDYcF95h7HoMTrC

## Solución:
Para obtener acceso al siguiente nivel, se debe usar el binario `setuid` que se encuentra en el directorio `home`. Se recomienda ejecutarlo sin argumentos para descubrir cómo se usa.

```bash
bandit19@bandit:~$ ls
bandit20-do
bandit19@bandit:~$ file bandit20-do
bandit20-do: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, BuildID[sha1]=c148b21f7eb7e816998f07490c8007567e51953f, for GNU/Linux 3.2.0, not stripped
bandit19@bandit:~$ ls -la
total 36
drwxr-xr-x  2 root     root      4096 Jan 11 19:18 .
drwxr-xr-x 70 root     root      4096 Jan 11 19:19 ..
-rwsr-x---  1 bandit20 bandit19 14876 Jan 11 19:18 bandit20-do
-rw-r--r--  1 root     root       220 Jan  6  2022 .bash_logout
-rw-r--r--  1 root     root      3771 Jan  6  2022 .bashrc
-rw-r--r--  1 root     root       807 Jan  6  2022 .profile
bandit19@bandit:~$
```

Lo ejecutamos sin argumentos para ver cómo se utiliza, y este nos indica que debemos especificar qué comando queremos utilizar, como si fuéramos otro usuario. En este caso, queremos ver la password del usuario `bandit20`:

```bash
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
VxCazJaVykI6W36BkBU0mJTCM8rR95XT
bandit19@bandit:~$
```

## Notas adicionales:
Para ejecutar scripts en linux se debe de hacer de la siguiente forma:

```bash
./nombre_script parametros
```

algunos scripts podrían solicitar permiso de superusuario (usuario root).

## Referencias:
- [setuid on Wikipedia](https://en.wikipedia.org/wiki/Setuid)
- https://www.linuxhispano.net/2010/08/02/cuatro-maneras-de-lanzar-un-script-en-linux/