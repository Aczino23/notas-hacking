## Objetivo:
There is a git repository at `ssh://bandit28-git@localhost/home/bandit28-git/repo`. The password for the user `bandit28-git` is the same as for the user `bandit28`.

Clone the repository and find the password for the next level.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit28
- **Password:** AVanL161y9rsbcJIsFHuw35rjaOM19nR

## Solución:
Clonamos el repositorio en un directorio dentro de `/tmp`:

```bash
bandit28@bandit:~$ mkdir /tmp/repo-tmp2
bandit28@bandit:~$ chmod 777 /tmp/repo-tmp2
bandit28@bandit:~$ cd /tmp/repo-tmp2
bandit28@bandit:/tmp/repo-tmp2$ git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit28/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit28/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit28-git@localhost's password:
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 2), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (9/9), done.
Resolving deltas: 100% (2/2), done.
bandit28@bandit:/tmp/repo-tmp2$
```

Revisamos el contenido del directorio `repo`:

```bash
bandit28@bandit:/tmp/repo-tmp2$ ls
repo
bandit28@bandit:/tmp/repo-tmp2$ cd repo/
bandit28@bandit:/tmp/repo-tmp2/repo$ ls
README.md
bandit28@bandit:/tmp/repo-tmp2/repo$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx

bandit28@bandit:/tmp/repo-tmp2/repo$
```

Al ver el archivo `README.md`, no encontramos nada útil, por lo tanto chequeamos el manual de `git` para ver qué nos puede ayudar a resolver el reto.

Dentro de los comandos útiles que encontramos, uno de ellos es `git log`, el cual, muestra los logs de cuando se ejecuta un `commit` en `git`:

También está el comando `git diff`, el que, nos indica los cambios entre `commits`:

Si hacemos un `git log`, vemos los `commit` realizados:

```bash
bandit28@bandit:/tmp/repo-tmp2/repo$ git log
commit 104db85a904e9691ff22aafe1a96124c88f75afa (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Tue Feb 21 22:03:10 2023 +0000

    fix info leak

commit 6c3c5e485cc531e5d52c321587ce1103833ab7c3
Author: Morla Porla <morla@overthewire.org>
Date:   Tue Feb 21 22:03:10 2023 +0000

    add missing data

commit cd3b97ef95879ec34df0d6c82f2a96d552f0e56c
Author: Ben Dover <noone@overthewire.org>
Date:   Tue Feb 21 22:03:10 2023 +0000

    initial commit of README.md
bandit28@bandit:/tmp/repo-tmp2/repo$
```

Vemos que tenemos deferentes commits por lo que comparamos el `commit` actual con el anterior para ver sus diferencias: 

```bash
bandit28@bandit:/tmp/repo-tmp2/repo$ git diff 104db85a904e9691ff22aafe1a96124c88f75afa 6c3c5e485cc531e5d52c321587ce1103833ab7c3
diff --git a/README.md b/README.md
index 5c6457b..b302105 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials

 - username: bandit29
-- password: xxxxxxxxxx
+- password: tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S

bandit28@bandit:/tmp/repo-tmp2/repo$
```

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| git log | El comando `git log` muestra todas las commits en el historial del repositorio |
| git diff | Muestra los cambios entre el árbol de trabajo y el índice o un árbol, los cambios entre el índice y un árbol, los cambios entre dos árboles, los cambios resultantes de una combinación, los cambios entre dos objetos blob o los cambios entre dos archivos en el disco. |

## Referencias:
- https://git-scm.com/docs/git-clone
