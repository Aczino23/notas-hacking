## Objetivo:
There is a git repository at `ssh://bandit27-git@localhost/home/bandit27-git/repo`. The password for the user `bandit27-git` is the same as for the user `bandit27`.

Clone the repository and find the password for the next level.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit27
- **Password:** YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS

## Solución:
Para poder clonar este repositorio, usamos la herramienta `git` con su opción `clone`, seguido de la ruta dada entre comillas para poder clonar el repositorio creamos una carpeta temporal en `/tmp`:

```bash
bandit27@bandit:/tmp/repo-tmp$ git clone ssh://bandit27-git@localhost/home/bandit27-git/repo
Cloning into 'repo'...
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit27/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit27/.ssh/known_hosts).

                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

!!! You are trying to log into this SSH server on port 22, which is not intended.

bandit27-git@localhost: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
bandit27@bandit:/tmp/repo-tmp$
```

Cuando intentamos clonar el repositorio nos maraca un error ya que no se esta especificando el puerto por lo tanto realizamos lo siguiente:

```bash
bandit27@bandit:/tmp/repo-tmp$ git clone ssh://bandit27git@localhost:2220/home/bandit27-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit27/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit27/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit27-git@localhost's password:
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
bandit27@bandit:/tmp/repo-tmp$
```

Luego de que el repositorio se encuentra clonado, revisamos su contenido y vemos que en el archivo `README` se encuentra la password del siguiente reto:

```bash
bandit27@bandit:/tmp/repo-tmp$ ls
repo
bandit27@bandit:/tmp/repo-tmp$ cd repo/
bandit27@bandit:/tmp/repo-tmp/repo$ ls
README
bandit27@bandit:/tmp/repo-tmp/repo$ cat README
The password to the next level is: AVanL161y9rsbcJIsFHuw35rjaOM19nR
bandit27@bandit:/tmp/repo-tmp/repo$
```

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| git | Git es un sistema de control de versiones distribuido, lo que significa que un clon local del proyecto es un repositorio de control de versiones completo. Estos repositorios locales plenamente funcionales permiten trabajar sin conexión o de forma remota con facilidad. |
| git clone | Clona un repositorio en un nuevo directorio |

## Referencias:
- https://es.wikipedia.org/wiki/Git
- https://git-scm.com/docs/git-clone