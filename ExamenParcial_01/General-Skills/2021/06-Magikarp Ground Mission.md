## Objetivo:
Do you know how to move between directories and read files in the shell? Start the container, `ssh` to it, and then `ls` once connected to begin. Login via `ssh` as `ctf-player` with the password, `a13b7f9d` Additional details will be available after launching your challenge instance.

**Hints:**
1. Finding a cheatsheet for bash would be really helpful!

## Solución:
1. para este reto se nos pide conectarnos por `ssh` a un servidor:

```bash
┌──(kali㉿kali)-[~]
└─$ ssh ctf-player@venus.picoctf.net -p 49174
The authenticity of host '[venus.picoctf.net]:49174 ([3.131.124.143]:49174)' can't be established.
ED25519 key fingerprint is SHA256:P1f6h95BrSVnJbm2AKhphfHHGEyAeThib/rN/AwKs24.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:4: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[venus.picoctf.net]:49174' (ED25519) to the list of known hosts.
ctf-player@venus.picoctf.net's password: 
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 5.4.0-1041-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ctf-player@pico-chall$
```

2. Una vez conectados en el servidor listamos los archivos y vemos que hay un archivo que contiene la primera parte de la bandera, luego vemos que hay otro archivo el cual al momento de mostrar su contenido nos da una pista para obtener la segunda parte de la bandera dicho archivo nos indica que nos dirijamos a la raíz del servidor. 

```bash
ctf-player@pico-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt
ctf-player@pico-chall$ cat 1of3.flag.txt 
picoCTF{xxsh_
ctf-player@pico-chall$ cat instructions-to-2of3.txt 
Next, go to the root of all things, more succinctly `/`
ctf-player@pico-chall$
```

3. Una vez que nos dirigimos a la rais del servidor listamos su contenido y vemos que hay un archivo que contiene la segunda parte de la bandera, en esta ocasión se nos vuelve a dar una pista para obtener la tercera y ultima parte de la bandera, dicha pista se nos indica en una archivo el cual nos dice que nos dirijamos a el `home` del usuario `ctf-player`:

```bash
ctf-player@pico-chall$ cd /
ctf-player@pico-chall$ ls
2of3.flag.txt  boot  etc   instructions-to-3of3.txt  lib64  mnt  proc  run   srv  tmp  var
bin            dev   home  lib                       media  opt  root  sbin  sys  usr
ctf-player@pico-chall$ cat 2of3.flag.txt 
0ut_0f_\/\/4t3r_
ctf-player@pico-chall$ cat instructions-to-3of3.txt 
Lastly, ctf-player, go home... more succinctly `~`
ctf-player@pico-chall$
```

4. Una vez en el `home` del usuario listamos su contenido y vemos que hay un archivo que contiene la ultima parte de la bandera.

```bash
ctf-player@pico-chall$ cd /home/ctf-player/
ctf-player@pico-chall$ ls
3of3.flag.txt  drop-in
ctf-player@pico-chall$ cat 3of3.flag.txt 
71be5264}
ctf-player@pico-chall$ 
```

###  **flag:** picoCTF{xxsh_0ut_0f_\/\/4t3r_71be5264}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| ssh | Es un protocolo de comunicación segura y que además da nombre al propio programa que usa en el que podemos conectar de forma remota con servidores que estén configurados para este tipo de conexión. La conexión SSH está cifrada de extremo a extremo además de necesitar una autenticación para poder conectar al servidor. |

## Referencias:
- https://es.wikipedia.org/wiki/Secure_Shell