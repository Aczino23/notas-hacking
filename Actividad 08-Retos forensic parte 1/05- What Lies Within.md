## Descripción: 
There's something in the [building](https://jupiter.challenges.picoctf.org/static/011955b303f293d60c8116e6a4c5c84f/buildings.png). Can you retrieve the flag?

**Pistas:**
1. There is data encoded somewhere... there might be an online decoder.

## Solución:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/What_Lies_Within]
└─$ ls
buildings.png
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/What_Lies_Within]
└─$ file buildings.png
buildings.png: PNG image data, 657 x 438, 8-bit/color RGBA, non-interlaced
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/What_Lies_Within]
└─$ open buildings.png
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/What_Lies_Within]
└─$ zsteg -a buildings.png | grep picoCTF
b1,rgb,lsb,xy       .. text: "picoCTF{h1d1ng_1n_th3_b1t5}"
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/What_Lies_Within]
└─$
```

### Flag: picoCTF{h1d1ng_1n_th3_b1t5}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| Zsteg | Zsteg también es una herramienta como Jsteg pero se usa para detectar esteganografía LSB solo en el caso de imágenes PNG y BMP. |

### ¿Qué significa el bit menos significativo (LSB)?

En informática, el bit menos significativo es el bit que está más alejado a la derecha y tiene el menor valor en un número binario de varios bits. Como los números binarios se utilizan en gran medida en la informática y otras áreas relacionadas, el bit menos significativo tiene importancia, especialmente cuando se trata de la transmisión de números binarios.

## Referencias:
- https://es.wikipedia.org/wiki/Bit_menos_significativo