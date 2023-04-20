# Tapping

## Descripción: 
Theres tapping coming in from the wires. What's it saying `nc jupiter.challenges.picoctf.org 9422`.

**Pistas:**
1. What kind of encoding uses dashes and dots?
2. The flag is in the format PICOCTF{}

## Solución:
1. En este reto se nos da un mensaje que al parecer esta cifrado en código morse: 

```bash
┌──(kali㉿kali)-[~]
└─$ nc jupiter.challenges.picoctf.org 9422
.--. .. -.-. --- -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. ..--- -.... ---.. ...-- ---.. ..--- ....- -.... .---- ----- } 

┌──(kali㉿kali)-[~]
└─$
```

2. Con ayuda de un decodificador de código morse en línea descodificamos el mensaje: [# Traductor Morse](https://morsedecoder.com/es/)

![Pasted image 20230420140643](Pasted%20image%2020230420140643.png)

### Flag: picoCTF{M0RS3C0D31SFUN2683824610}

## Notas adicionales:

## ¿Qué es el código morse?
El código morse, clave morse o alfabeto morse **es un sistema internacional de representación de caracteres a través de una serie de señales emitidas de manera intermitente**. Dichas señales pueden ser cortas o largas y se transcriben a través de puntos (.) y guiones (-) respectivamente, separados entre sí por espacios en blanco. Los caracteres que representan son, esencialmente, letras y números.

## Referencias:
- https://morsedecoder.com/es/