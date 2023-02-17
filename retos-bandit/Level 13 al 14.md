## Objetivo:
The password for the next level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. **Note:** **localhost** is a hostname that refers to the machine you are working on.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit13
- **Password:** wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw

## Solución:
Revisamos que encontramos en el directorio `home` del usuario `bandit13`:

```bash
bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$
```

Nos conectamos usando esta llave privada. Para indicar la `private key` al momento de conectarse por SSH, se usa la opción `-i`, y nos conectamos al `localhost` (este se refiere al hostname de la máquina en la cual estamos conectados):

```bash
bandit13@bandit:~$ ssh -i sshkey.private bandit14@localhost -p 2220
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit13/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit13/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|

bandit14@bandit:~$ ls
bandit14@bandit:~$
```

Ahora revisamos el directorio `/etc/bandit_pass/bandit14` para encontrar la password de `bandit14`:

```bash
bandit14@bandit:~$ ls /etc/bandit_pass
bandit0   bandit13  bandit18  bandit22  bandit27  bandit31  bandit6
bandit1   bandit14  bandit19  bandit23  bandit28  bandit32  bandit7
bandit10  bandit15  bandit2   bandit24  bandit29  bandit33  bandit8
bandit11  bandit16  bandit20  bandit25  bandit3   bandit4   bandit9
bandit12  bandit17  bandit21  bandit26  bandit30  bandit5
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
bandit14@bandit:~$
```

## Notas adicionales:

| Comando | Descripción |
| --- | --- |
| ssh | El comando **ssh** ofrece comunicación encriptada y segura entre dos sistemas sobre una red no segura. Este comando reemplaza al **telnet**, **rlogin**, **rsh**. |

## Referencias:
- [SSH/OpenSSH/Keys](https://help.ubuntu.com/community/SSH/OpenSSH/Keys)