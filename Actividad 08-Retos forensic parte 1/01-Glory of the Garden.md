## Descripción: 
This [garden](https://jupiter.challenges.picoctf.org/static/d0e1ffb10fc0017c6a82c57900f3ffe3/garden.jpg) contains more than it seems.

**Pistas:**
1. What is a hex editor?

## Solución:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Glory_of_the_Garden]
└─$ file garden.jpg                                                                                              
garden.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 72x72, segment length 16, baseline, precision 8, 2999x2249, components 3
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Glory_of_the_Garden]
└─$ strings garden.jpg | grep picoCTF
Here is a flag "picoCTF{more_than_m33ts_the_3y3eBdBd2cc}"
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Glory_of_the_Garden]
└─$ 
```

### Flag:  picoCTF{more_than_m33ts_the_3y3eBdBd2cc}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| strings | Muestra las cadenas de caracteres imprimibles que haya en ficheros |

## Referencias:
- https://www.howtogeek.com/427805/how-to-use-the-strings-command-on-linux/