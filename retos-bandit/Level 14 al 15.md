## Objetivo:
The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit14
- **Password:** fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq

## Solución:
Para realizar una conexión a nosotros mismos, podemos usar el comando netcat (`nc`); o `telnet`, donde se indica el hostname `localhost`, y el puerto `30000`:

```bash
bandit14@bandit:~$ nc localhost 30000
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
Correct!
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

^C
bandit14@bandit:~$
```

```bash
bandit14@bandit:~$ telnet localhost 30000
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
Correct!
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

Connection closed by foreign host.
bandit14@bandit:~$
```

## Notas adicionales:

| Comando | Descripción |
| --- | --- |
| nc | Mediante el comando `nc` puedes conectarte a los puertos **TCP/UDP** de un host. De este modo podrás conectarte otros servidores usando diferentes protocolos de red. |
| telnet | Telnet es un protocolo obsoleto que se utiliza para iniciar sesión de forma remota en otra computador o equipo de comunicación a través de una red. El protocolo Telnet no ofrece seguridad. |


## Referencias:
-  [How the Internet works in 5 minutes (YouTube)](https://www.youtube.com/watch?v=7_LPdttKXPc) 
-   [IP Addresses](http://computer.howstuffworks.com/web-server5.htm)
-   [IP Address on Wikipedia](https://en.wikipedia.org/wiki/IP_address)
-   [Localhost on Wikipedia](https://en.wikipedia.org/wiki/Localhost)
-   [Ports](http://computer.howstuffworks.com/web-server8.htm)
-   [Port (computer networking) on Wikipedia](https://en.wikipedia.org/wiki/Port_(computer_networking))