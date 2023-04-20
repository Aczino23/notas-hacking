# The Numbers

## Descripción: 
The [numbers](https://jupiter.challenges.picoctf.org/static/f209a32253affb6f547a585649ba4fda/the_numbers.png)... what do they mean?

**Pistas:**
1. The flag is in the format PICOCTF{}

## Solución:
1. En este reto se nos da una imagen con algunos números escritos en ella. Del formato de imagen “algunos números { más números }” podemos suponer que al decodificarlos podríamos obtener la bandera.

![Pasted image 20230420115010](Pasted%20image%2020230420115010.png)

2. Al poner la cadena en https://www.dcode.fr/cipher-identifier, llegamos a saber que esto es solo un cifrado A1Z26, es decir, un texto cifrado de alfabeto a número y de número a alfabeto.

> 16 9 3 15 3 20 6 => PICOCTF

> 20 8 5 14 21 13 2 5 18 19 13 1 19 15 14 => THENUMBERSMASON

### Flag: picoCTF{THENUMBERSMASON}

## Notas adicionales:

**¿Qué es el cifrado A1Z26?** (Definición) El **Cifrado de letra a número** (o Número a Letra Cifrado o alfabeto numerado) consiste en reemplazar cada letra por su posición en el alfabeto, por ejemplo A=1, B=2, Z=26, de ahí su sobrenombre A1Z26.

## Referencias:
- https://www.dcode.fr/letter-number-cipher