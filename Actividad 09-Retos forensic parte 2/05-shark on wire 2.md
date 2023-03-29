## Descripción: 
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/b506393b6f9d53b94011df000c534759/capture.pcap). Recover the flag that was pilfered from the network.

**Pistas:**

## Solución:
1. En este reto se nos da una captura de paquetes: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/shark_on_wire_2]
└─$ ls
capture.pcap

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/shark_on_wire_2]
└─$ file capture.pcap
capture.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 262144)

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/shark_on_wire_2]
└─$ 
```

2.  Con ayuda de la herramienta **Wireshark** analizamos la captura de paquetes y vemos que tenemos el trafico de red con diferentes protocolos:   

![Pasted image 20230328205421](Pasted%20image%2020230328205421.png)

3. Siguiendo el stream de los paquetes UDP nos damos cuenta que en el stream 32 se encuentra la palabra **start** y en el stream 60 se encuentra la palabra **end** lo que no da una pista sobre en donde se podría encontrar la flag: 

![Pasted image 20230328210310](Pasted%20image%2020230328210310.png)

![Pasted image 20230328210356](Pasted%20image%2020230328210356.png)

4. Entonces lo siguiente que hacemos es filtrar los paquetes UDP en los que el puerto destino sea el puerto 22: 

![Pasted image 20230328210818](Pasted%20image%2020230328210818.png)

5. Analizando u observando la información de los paquetes UDP nos damos cuenta que inicia el 5000 y termina en 5000 y que va variando, por lo tanto descubrimos que en dicha información se encuentra la flag: 

![Pasted image 20230328211533](Pasted%20image%2020230328211533.png)

6. Entonces con script de Python obtenemos la flag: 

```python
from scapy.all import *

paquetes = rdpcap('capture.pcap')

flag = ''

for p in paquetes:
        if UDP in p and p[UDP].dport == 22:
                #print(p)
                if p[UDP].sport > 5000:
                        flag += chr(p[UDP].sport - 5000)

print(flag)
```

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/shark_on_wire_2]
└─$ python3 exp.py
picoCTF{p1LLf3r3d_data_v1a_st3g0}

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/shark_on_wire_2]
└─$ 
```

### Flag: picoCTF{p1LLf3r3d_data_v1a_st3g0}

## Notas adicionales:

### Paquetes UDP:
El **Protocolo de datagrama de usuario (UDP)** es un protocolo ligero de transporte de datos que funciona sobre IP.
UDP proporciona un mecanismo para detectar datos corruptos en paquetes, pero _no_ intenta resolver otros problemas que surgen con paquetes, como cuando se pierden o llegan fuera de orden. Por eso, a veces UDP es conocido como el **protocolo de datos _no confiable_** .

### Wireshark:
La herramienta intercepta el tráfico y lo convierte en un **formato legible para las personas**. Esto hace que sea más fácil identificar qué tráfico está cruzando la red, con qué frecuencia y la latencia que hay entre ciertos saltos. Si bien Wireshark admite más de 2.000 protocolos de red, muchos de ellos inusuales o antiguos, los profesionales encuentran una gran utilidad en el análisis de identidades IP. La mayoría de los paquetes son **TCP, UPD e ICMP.**

## Referencias:
- https://es.wikipedia.org/wiki/Wireshark
- https://scapy.net/