## Descripción: 
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/483e50268fe7e015c49caf51a69063d0/capture.pcap). Recover the flag.

**Pistas:**
1. Try using a tool like Wireshark
2. What are streams?

## Solución:

1. En este reto se nos da una captura de paquetes: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/shark_on_wire_1]
└─$ ls
capture.pcap
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/shark_on_wire_1]
└─$ file capture.pcap 
capture.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 262144)
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/shark_on_wire_1]
└─$ open capture.pcap 
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/shark_on_wire_1]
└─$ 
```

2. Con ayuda de la herramienta **Wireshark** seguimos la secuencia (streams) de los paquetes UDP y vemos que en uno de ellos se encuentra la flag:

![Pasted image 20230323122606](Pasted%20image%2020230323122606.png)

### Flag:  picoCTF{StaT31355_636f6e6e}

## Notas adicionales:

### Paquetes UDP:
El **Protocolo de datagrama de usuario (UDP)** es un protocolo ligero de transporte de datos que funciona sobre IP.
UDP proporciona un mecanismo para detectar datos corruptos en paquetes, pero _no_ intenta resolver otros problemas que surgen con paquetes, como cuando se pierden o llegan fuera de orden. Por eso, a veces UDP es conocido como el **protocolo de datos _no confiable_** .

### Wireshark:
La herramienta intercepta el tráfico y lo convierte en un **formato legible para las personas**. Esto hace que sea más fácil identificar qué tráfico está cruzando la red, con qué frecuencia y la latencia que hay entre ciertos saltos. Si bien Wireshark admite más de 2.000 protocolos de red, muchos de ellos inusuales o antiguos, los profesionales encuentran una gran utilidad en el análisis de identidades IP. La mayoría de los paquetes son **TCP, UPD e ICMP.**

## Referencias:
- https://es.wikipedia.org/wiki/Wireshark