## Descripción: 
We found this [file](https://jupiter.challenges.picoctf.org/static/ab30fcb7d47364b4190a7d3d40edb551/mystery). Recover the flag.

**Pistas:**
1. Try fixing the file header

## Solución:
1. En este reto se nos proporciona un archivo que al parecer esta dañado: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ ls
mystery
                                                                                           
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ file mystery       
mystery: data
                                                                                           
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ xxd mystery | head      
00000000: 8965 4e34 0d0a b0aa 0000 000d 4322 4452  .eN4........C"DR
00000010: 0000 066a 0000 0447 0802 0000 007c 8bab  ...j...G.....|..
00000020: 7800 0000 0173 5247 4200 aece 1ce9 0000  x....sRGB.......
00000030: 0004 6741 4d41 0000 b18f 0bfc 6105 0000  ..gAMA......a...
00000040: 0009 7048 5973 aa00 1625 0000 1625 0149  ..pHYs...%...%.I
00000050: 5224 f0aa aaff a5ab 4445 5478 5eec bd3f  R$......DETx^..?
00000060: 8e64 cd71 bd2d 8b20 2080 9041 8302 08d0  .d.q.-.  ..A....
00000070: f9ed 40a0 f36e 407b 9023 8f1e d720 8b3e  ..@..n@{.#... .>
00000080: b7c1 0d70 0374 b503 ae41 6bf8 bea8 fbdc  ...p.t...Ak.....
00000090: 3e7d 2a22 336f de5b 55dd 3d3d f920 9188  >}*"3o.[U.==. ..
                                                                                           
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$
```

2. Al parecer los primeros bytes de la cabecera del archivo están mal, entonces con ayuda de la herramienta **hexeditor** reparamos la cabecera del archivo:  

![Pasted image 20230326215222](Pasted%20image%2020230326215222.png)

3. Una vez que corregimos la cabecera verificamos que el archivo aun no es reconocido al parecer ahora se trata de los **Chunks**:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ file mystery
mystery: data
                                                                                                   
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ xxd mystery | head 
00000000: 8950 4e47 0d0a 1a0a 0000 000d 4322 4452  .PNG........C"DR
00000010: 0000 066a 0000 0447 0802 0000 007c 8bab  ...j...G.....|..
00000020: 7800 0000 0173 5247 4200 aece 1ce9 0000  x....sRGB.......
00000030: 0004 6741 4d41 0000 b18f 0bfc 6105 0000  ..gAMA......a...
00000040: 0009 7048 5973 aa00 1625 0000 1625 0149  ..pHYs...%...%.I
00000050: 5224 f0aa aaff a5ab 4445 5478 5eec bd3f  R$......DETx^..?
00000060: 8e64 cd71 bd2d 8b20 2080 9041 8302 08d0  .d.q.-.  ..A....
00000070: f9ed 40a0 f36e 407b 9023 8f1e d720 8b3e  ..@..n@{.#... .>
00000080: b7c1 0d70 0374 b503 ae41 6bf8 bea8 fbdc  ...p.t...Ak.....
00000090: 3e7d 2a22 336f de5b 55dd 3d3d f920 9188  >}*"3o.[U.==. ..
                                                                                                   
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ 
```

4. Con ayuda de la herramienta **hexeditor** reparamos los **Chunks** del archivo:  

![Pasted image 20230326215821](Pasted%20image%2020230326215821.png)

5. Ahora ya el archivo es reconocido como una imagen pero al momento de abrirla se obtiene un error, entones con ayuda de la herramienta `pngcheck` vemos de que error se trata:  

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ file mystery                   
mystery: PNG image data, 1642 x 1095, 8-bit/color RGB, non-interlaced
                                                                                                   
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ open mystery                   
                                                                                                   
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ pngcheck -v mystery            
File: mystery (202940 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1642 x 1095 image, 24-bit RGB, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 2852132389x5669 pixels/meter
  CRC error in chunk pHYs (computed 38d82c82, expected 495224f0)
ERRORS DETECTED in mystery
                                                                                                   
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ 
```

6. Reparamos los **Chunks** y su longitud y verificamos que la imagen ahora ya no contiene errores: 

![Pasted image 20230326221420](Pasted%20image%2020230326221420.png)

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ pngcheck -v mystery
File: mystery (202940 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1642 x 1095 image, 24-bit RGB, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 5669x5669 pixels/meter (144 dpi)
  chunk IDAT at offset 0x00057, length 65445
    zlib: deflated, 32K window, fast compression
  chunk IDAT at offset 0x10008, length 65524
  chunk IDAT at offset 0x20008, length 65524
  chunk IDAT at offset 0x30008, length 6304
  chunk IEND at offset 0x318b4, length 0
No errors detected in mystery (9 chunks, 96.3% compression).
                                                                                                   
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/c0rrupt]
└─$ 
```

7. Ahora si abrimos la imagen vemos que ahí se encuentra la flag: 

![Pasted image 20230326221716](Pasted%20image%2020230326221716.png)

### Flag: picoCTF{c0rrupt10n_1847995}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| pngcheck  | Verifica la integridad de los archivos PNG, JNG y MNG (verificando los CRC internos de 32 bits, también conocidos como sumas de verificación, y descomprimiendo los datos de la imagen); opcionalmente, puede volcar casi toda la información de nivel de fragmento en la imagen en forma legible por humanos. Por ejemplo, se puede utilizar para imprimir las estadísticas básicas sobre una imagen (dimensiones, profundidad de bits, etc.); para enumerar la información de color y transparencia en su paleta (suponiendo que tenga una); o para extraer las anotaciones de texto incrustadas. Este es un programa de línea de comandos con capacidades por lotes. |
| hexeditor | Es un editor de archivos binarios confiable y muy fácil de usar. Este visor hexadecimal de Linux se presenta con muchas opciones, por ejemplo, búsqueda / comparación rápida, resaltador, EBCDIC, esquemas de color, ajuste automático, modos INS / OVR, marcadores, seguimiento de cambios. Su cambiador de pantalla tiene más de setenta propiedades como fechas, flotantes, enteros y muchos más. |

## Referencias:
- https://en.wikipedia.org/wiki/List_of_file_signatures