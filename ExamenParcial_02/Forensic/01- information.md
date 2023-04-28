# information

## Descripción: 
Files can always be changed in a secret way. Can you find the flag? [cat.jpg](https://mercury.picoctf.net/static/e5825f58ef798fdd1af3f6013592a971/cat.jpg)

**Pistas:**
1. Look at the details of the file
2. Make sure to submit the flag as picoCTF{XXXXX}

## Solución:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/information]
└─$ ls
cat.jpg

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/information]
└─$ exiftool cat.jpg                       
ExifTool Version Number         : 12.57
File Name                       : cat.jpg
Directory                       : .
File Size                       : 878 kB
File Modification Date/Time     : 2021:03:15 14:24:46-04:00
File Access Date/Time           : 2023:04:27 20:11:18-04:00
File Inode Change Date/Time     : 2023:04:27 20:11:18-04:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617
Copyright Notice                : PicoCTF
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 10.80
License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
Rights                          : PicoCTF
Image Width                     : 2560
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2560x1598
Megapixels                      : 4.1

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/information]
└─$ echo "cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9" | base64 -d
picoCTF{the_m3tadata_1s_modified}  

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/information]
└─$ 
```

### Flag: picoCTF{the_m3tadata_1s_modified} 

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| exiftool | **ExifTool** es una biblioteca **Perl** independiente de la plataforma, más una aplicación de línea de comandos para leer, escribir y editar **metainformación** en una amplia variedad de archivos.|

## ¿Qué son los metadatos?

Los metadatos también son definidos como aquellos datos que dan información sobre los datos en cuestión; es decir, estos metadatos caracterizan o describen el contenido de los archivos.

Una definición más técnica es la que ofrece la entidad de NISO (National Information Standards Organization)), que define metadato como aquella información estructurada, la cual, describe, explica, localiza o facilita de algún modo la recuperación, el uso o la gestión de la información.

## Referencias:
- https://www.adslzone.net/reportajes/tecnologia/metadatos-que-son/