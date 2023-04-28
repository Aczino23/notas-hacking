# Wireshark doo dooo do doo...

## Descripción: 
Can you find the flag? [shark1.pcapng](https://mercury.picoctf.net/static/81c7862241faf4a48bd64a858392c92b/shark1.pcapng).

**Pistas:** 

## Solución:
1. Para resolver este reto, se nos da un archivo de paquetes de red, y como dice el nombre del reto, utilizaremos `Wireshark`.
 
![Pasted image 20230427193152](Pasted%20image%2020230427193152.png)

3. Para empezar, analizaremos los diferentes streams de los paquetes TCP, ya que en general, ahi encontramos la flag.
4. Al llegar al stream 5, encontramos la flag codificada en ROT13:

![Pasted image 20230427193300](Pasted%20image%2020230427193300.png)

```txt
flag codificada: Gur synt vf cvpbPGS{c33xno00_1_f33_h_qrnqorrs}
```

5.  Después de decodificarlo con [Cyberchef](https://gchq.github.io/CyberChef/#recipe=ROT13(true,true,false,13)&input=R3VyIHN5bnQgdmYgY3ZwYlBHU3tjMzN4bm8wMF8xX2YzM19oX3FybnFvcnJzfQ), encontramos que la flag es:

```txt
The flag is picoCTF{p33kab00_1_s33_u_deadbeef}
```

### Flag: picoCTF{p33kab00_1_s33_u_deadbeef}

## Notas adicionales:

### Wireshark:
La herramienta intercepta el tráfico y lo convierte en un **formato legible para las personas**. Esto hace que sea más fácil identificar qué tráfico está cruzando la red, con qué frecuencia y la latencia que hay entre ciertos saltos. Si bien Wireshark admite más de 2.000 protocolos de red, muchos de ellos inusuales o antiguos, los profesionales encuentran una gran utilidad en el análisis de identidades IP. La mayoría de los paquetes son **TCP, UPD e ICMP.**

## Protocolo TCP:
El Protocolo de Control de Transmisión (Transmission Control Protocol en inglés o TCP) es el método de comunicación de datos por defecto entre distintos dispositivos, a través de una red. Este establece y mantiene una conexión entre el emisor y el receptor durante el proceso de transferencia.

## Referencias:
- https://www.hostinger.mx/tutoriales/protocolo-tcp?ppc_campaign=google_search_generic_hosting_all&bidkw=defaultkeyword&lo=9073791