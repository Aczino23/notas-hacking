## Descripción: 
This is a really weird text file [TXT](https://jupiter.challenges.picoctf.org/static/e7e5d188621ee705ceeb0452525412ef/flag.txt)? Can you find the flag?

**Pistas:**
1. How do operating systems know what kind of file it is? (It's not just the ending!
2. Make sure to submit the flag as picoCTF{XXXXX}

## Solución:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/extensions]
└─$ ls
flag.txt
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/extensions]
└─$ file flag.txt    
flag.txt: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/extensions]
└─$ xxd -l 32 flag.txt           
00000000: 8950 4e47 0d0a 1a0a 0000 000d 4948 4452  .PNG........IHDR
00000010: 0000 06a1 0000 0260 0802 0000 0085 ad5e  .......`.......^
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/extensions]
└─$ 
```

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/extensions]
└─$ mv flag.txt flag.png
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/extensions]
└─$ ls
flag.png
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/extensions]
└─$ file flag.png  
flag.png: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/extensions]
└─$ open flag.png 
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/extensions]
└─$
```

### Flag: 

![Pasted image 20230323124117](Pasted%20image%2020230323124117.png)

## Notas adicionales:

### Magic bytes:
El byte mágico no es más que los primeros bytes de un archivo que se utiliza para reconocer un archivo. No es visible si abre el archivo. Pero se puede ver usando algunas herramientas especiales. Todas las variantes de Linux tienen una herramienta llamada archivo que le dice qué tipo de archivo es. Como se muestra a continuación, este es un archivo .jpg.

## Referencias:
- https://en.wikipedia.org/wiki/List_of_file_signatures