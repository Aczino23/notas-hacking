## Objetivo:
There is a git repository at `ssh://bandit30-git@localhost/home/bandit30-git/repo`. The password for the user `bandit30-git` is the same as for the user `bandit30`.

Clone the repository and find the password for the next level.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit30
- **Password:** xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS

## Solución:
Clonamos el repositorio en un directorio dentro de `/tmp`:

```bash
bandit30@bandit:~$ mkdir /tmp/repo-tmp4
bandit30@bandit:~$ chmod 777 /tmp/repo-tmp4
bandit30@bandit:~$ cd /tmp/repo-tmp4
bandit30@bandit:/tmp/repo-tmp4$ ls
bandit30@bandit:/tmp/repo-tmp4$ git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit30/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit30/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit30-git@localhost's password:
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
Receiving objects: 100% (4/4), 298 bytes | 298.00 KiB/s, done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
bandit30@bandit:/tmp/repo-tmp4$
```

Revisamos el contenido del directorio `repo`:

```bash
bandit30@bandit:/tmp/repo-tmp4$ ls
repo
bandit30@bandit:/tmp/repo-tmp4$ cd repo/
bandit30@bandit:/tmp/repo-tmp4/repo$ ls
README.md
bandit30@bandit:/tmp/repo-tmp4/repo$ cat README.md
just an epmty file... muahaha
bandit30@bandit:/tmp/repo-tmp4/repo$
```

Al ver el archivo `README.md`, no encontramos nada útil, por lo tanto vemos los logs de los cambios del repo:

```bash
bandit30@bandit:/tmp/repo-tmp4/repo$ git log
commit cf552c166d78421e64ddf52f850e680075d216e1 (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Tue Feb 21 22:03:13 2023 +0000

    initial commit of README.md
bandit30@bandit:/tmp/repo-tmp4/repo$
```

Como podemos ver, solo tiene el `commit` inicial, por lo tanto, revisamos si tiene más `branch`:

```bash
bandit30@bandit:/tmp/repo-tmp4/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
bandit30@bandit:/tmp/repo-tmp4/repo
```

Pero al chequear, nos damos cuenta que solo se muestra el `branch master`. Otra cosa que podemos ver, es si no se ocultaron ramas usando el comando `git stash`. Este oculta el branch y los deja como referencias.
Para poder ver estas referencias, se usa el comando `git show-ref`:

```bash
bandit30@bandit:/tmp/repo-tmp4/repo$ git show-ref
cf552c166d78421e64ddf52f850e680075d216e1 refs/heads/master
cf552c166d78421e64ddf52f850e680075d216e1 refs/remotes/origin/HEAD
cf552c166d78421e64ddf52f850e680075d216e1 refs/remotes/origin/master
831aac2e2341f009e40e46392a4f5dd318483019 refs/tags/secret
bandit30@bandit:/tmp/repo-tmp4/repo$
```

Vemos que aparece la referencia `refs/tags/secret`, si vemos que contiene con `git show f17132340e8ee6c159e0a4a6bc6f80e1da3b1aea`, nos muestra las password del siguiente reto:

```bash
bandit30@bandit:/tmp/repo-tmp4/repo$ git show 831aac2e2341f009e40e46392a4f5dd318483019
OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt
bandit30@bandit:/tmp/repo-tmp4/repo$
```

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| git show | es una herramienta de línea de comandos que se utiliza para ver detalles ampliados de objetos de Git, como blobs, árboles, etiquetas y confirmaciones, y que presenta un comportamiento específico para cada tipo de objeto. | 
| git show-ref | Muestra las referencias disponibles en un repositorio local junto con las identificaciones de confirmación asociadas.Los resultados pueden ser filtrados usando un patrón y las etiquetas pueden ser desviadas hacia las identificaciones de los objetos.Además,puede utilizarse para comprobar si existe una referencia en particular. |

## Referencias:
- https://git-scm.com/doc