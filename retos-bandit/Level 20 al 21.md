## Objetivo:
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

**NOTE:** Try connecting to your own network daemon to see if it works as you think

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit20
- **Password:** VxCazJaVykI6W36BkBU0mJTCM8rR95XT

## Solución:
Vemos que existe el archivo `setuid` en el directorio home:

```bash
bandit20@bandit:~$ ls -l
total 16
-rwsr-x--- 1 bandit21 bandit20 15600 Jan 11 19:18 suconnect
bandit20@bandit:~$
```

Si vemos las instrucciones del software, este indica que solo se debe ingresar el puerto de conexión:

```bash
bandit20@bandit:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
bandit20@bandit:~$
```

Para usar este comando, en el terminal escribimos `tmux` y damos `enter`, lo que nos mostrará una nueva terminal. Para poder dividirla, usamos la combinación de teclas `CTRL+b`, seguido del símbolo `%`. Esto nos dividirá de forma vertical el terminal.

Para movernos entre terminales, usamos `CTRL+b` con las teclas de dirección.

Ahora que podemos trabajar con dos terminales, creamos un `listener` usando `nc`, donde, la opción `-l` es para dejar al equipo en modo escucha, y la opción `-p 2023` para escuchar en el puerto `2023`.

Pero cómo se debe pasar la password del reto anterior, lo hacemos mediante el comando `echo` (también puede ser mediante el comando `cat`).

Una vez arriba el listener, en el otro terminal usamos el binario suconnect al puerto definido para poder obtener la password del siguiente reto:

```bash
bandit20@bandit:~$ echo "VxCazJaVykI6W36BkBU0mJTCM8rR95XT" | nc -l -p 2023
NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
bandit20@bandit:~$ 
```

```bash
bandit20@bandit:~$ ./suconnect 2023
Read: VxCazJaVykI6W36BkBU0mJTCM8rR95XT
Password matches, sending next password
bandit20@bandit:~$ 
```

## Notas adicionales:
Un `listener` usando `nc`, donde, la opción `-l` es para dejar al equipo en modo escucha, y la opción `-p` para escuchar en un puerto especifico.

## Referencias:
- https://cloudzy.com/knowledge-base/netcat-listener/
- https://www.sciencedirect.com/topics/computer-science/netcat-listener