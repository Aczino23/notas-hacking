# Packets Primer

## Descripción: 
Download the packet capture file and use packet analysis software to find the flag.
-   [Download packet capture](https://artifacts.picoctf.net/c/196/network-dump.flag.pcap)

**Pistas:**
1. Wireshark, if you can install and use it, is probably the most beginner friendly packet analysis software product.

## Solución:
1. Como nos dice la pista, para resolver este reto necesitaremos utilizar `Wireshark` para poder analizar el archivo de paquetes de red.

2. Al estar dentro del software, vemos solo 5 paquetes, por lo que será fácil encontrar la flag.

3. Al darle click derecho a un paquete TCP, le damos en `follow` -> `TCP stream`, donde podremos ver la flag:

![Pasted image 20230427200104](Pasted%20image%2020230427200104.png)

4. Usando `echo` en Linux le quitamos los espacio a la cadena y obtenemos la bandera: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Packets_Primer]
└─$ echo "p i c o C T F { p 4 c k 3 7 _ 5 h 4 r k _ 0 1 b 0 a 0 d 6 }" | sed 's/ //g' 
picoCTF{p4ck37_5h4rk_01b0a0d6}
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Packets_Primer]
└─$
```

### Flag: picoCTF{p4ck37_5h4rk_01b0a0d6}

## Notas adicionales:

### Wireshark:
La herramienta intercepta el tráfico y lo convierte en un **formato legible para las personas**. Esto hace que sea más fácil identificar qué tráfico está cruzando la red, con qué frecuencia y la latencia que hay entre ciertos saltos. Si bien Wireshark admite más de 2.000 protocolos de red, muchos de ellos inusuales o antiguos, los profesionales encuentran una gran utilidad en el análisis de identidades IP. La mayoría de los paquetes son **TCP, UPD e ICMP.**

## Protocolo TCP:
El Protocolo de Control de Transmisión (Transmission Control Protocol en inglés o TCP) es el método de comunicación de datos por defecto entre distintos dispositivos, a través de una red. Este establece y mantiene una conexión entre el emisor y el receptor durante el proceso de transferencia.

## Referencias: