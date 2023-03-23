## Descripción: 
Find the flag in this [picture](https://jupiter.challenges.picoctf.org/static/89b371a46702a31aa9931a2a2b12f8bf/pico_img.png).

**Pistas:**
1.  What does meta mean in the context of files?
2. Ever heard of metadata?

## Solución:
1. Solución #1:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/So_Meta]
└─$ ls
pico_img.png
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/So_Meta]
└─$ open pico_img.png 
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/So_Meta]
└─$ file pico_img.png 
pico_img.png: PNG image data, 600 x 600, 8-bit/color RGB, non-interlaced
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/So_Meta]
└─$ strings pico_img.png | grep picoCTF 
picoCTF{s0_m3ta_eb36bf44}
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/So_Meta]
└─$ 
```

2. Solución #2:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/So_Meta]
└─$ exiftool pico_img.png | grep picoCTF
Artist                          : picoCTF{s0_m3ta_eb36bf44}
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/So_Meta]
└─$
```

### Flag: picoCTF{s0_m3ta_eb36bf44} 

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| strings | Muestra las cadenas de caracteres imprimibles que haya en ficheros |
| exiftool | **ExifTool** es una biblioteca **Perl** independiente de la plataforma, más una aplicación de línea de comandos para leer, escribir y editar **metainformación** en una amplia variedad de archivos.|

### Que son los metadatos:
Podemos definir el término **metadatos** como datos que describen otros datos o «**datos sobre datos**«. Es decir, el concepto de metadatos se refiere a aquellos datos que aportan más información sobre los datos y describen el contenido de los ficheros o la información de los mismos incluso los cambios realizados en una imagen editada. Y estos datos, además de acompañar nuestras fotos o videos, también aportan información sobre los documentos ofimáticos, como fórmulas en una hoja de cálculo de **Calc** o **Excel**.

## Referencias:
- https://www.howtogeek.com/427805/how-to-use-the-strings-command-on-linux/
