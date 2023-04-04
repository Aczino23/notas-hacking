# Matryoshka doll

## Descripción: 
Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: [this](https://mercury.picoctf.net/static/b6205dd933ec01c022c4e6acbdf11116/dolls.jpg)

**Pistas:**
1. Wait, you can hide files inside files? But how do you find them?
2. Make sure to submit the flag as picoCTF{XXXXX}

## Solución:
1. En este reto se nos da una imagen que al parecer tiene mas imágenes escondidas en ella: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Matryoshka_doll]
└─$ ls
dolls.jpg

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Matryoshka_doll]
└─$ file dolls.jpg
dolls.jpg: PNG image data, 594 x 1104, 8-bit/color RGBA, non-interlaced

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Matryoshka_doll]
└─$ strings -n 10 dolls.jpg
eiCCPICC Profile
Screenshot
iTXtXML:com.adobe.xmp
<x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 5.4.0">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:exif="http://ns.adobe.com/exif/1.0/">
         <exif:PixelXDimension>594</exif:PixelXDimension>
         <exif:UserComment>Screenshot</exif:UserComment>
         <exif:PixelYDimension>1104</exif:PixelYDimension>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
IDEEb^*Qcb4
Z9vT?vA/_$
a#;s;[gyjD
n3zY[>GAD
=,e< =*?Yp
3Sn'&bbGf'
\sMKn$R`eG
~wkwwG;~A
base_images/2_c.jpgUT
C}-Zjvj"""Z
/\6c7l*18Mj
Hr~&    8Ja7i,
t+Vp`B2AYq
se\45~|_4Z
%(oQ1y~?e?
Db^!u"tE=O
9)IZ9Rj|Fn
|YrAkJI_S,
cG3CKkcs3G
=T*N+b_Io8
-8(Ly<7-"`
kT_S0/,0L3
mlKszlh<f$
>,\vxk~[        .R
l_(ZU2&?IX
>KO<K-j3|sD
base_images/2_c.jpgUT

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Matryoshka_doll]
└─$
```

2. Usando la herramienta **binwalk** extremaos las imágenes que hay dentro de las imagen original: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Matryoshka_doll]
└─$ binwalk -e dolls.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378950, uncompressed size: 383938, name: base_images/2_c.jpg
651608        0x9F158         End of Zip archive, footer length: 22

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Matryoshka_doll]
└─$ ls
dolls.jpg  _dolls.jpg.extracted

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Matryoshka_doll]
└─$ cd _dolls.jpg.extracted 

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Matryoshka_doll/_dolls.jpg.extracted]
└─$ ls
4286C.zip  base_images

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Matryoshka_doll/_dolls.jpg.extracted]
└─$ cd base_images         

┌──(kali㉿kali)-[~/…/forensics/Matryoshka_doll/_dolls.jpg.extracted/base_images]
└─$ ls
2_c.jpg

┌──(kali㉿kali)-[~/…/forensics/Matryoshka_doll/_dolls.jpg.extracted/base_images]
└─$ binwalk -e 2_c.jpg     

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 526 x 1106, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
187707        0x2DD3B         Zip archive data, at least v2.0 to extract, compressed size: 196043, uncompressed size: 201445, name: base_images/3_c.jpg
383805        0x5DB3D         End of Zip archive, footer length: 22
383916        0x5DBAC         End of Zip archive, footer length: 22

┌──(kali㉿kali)-[~/…/forensics/Matryoshka_doll/_dolls.jpg.extracted/base_images]
└─$ ls
2_c.jpg  _2_c.jpg.extracted

┌──(kali㉿kali)-[~/…/forensics/Matryoshka_doll/_dolls.jpg.extracted/base_images]
└─$ cd _2_c.jpg.extracted  

┌──(kali㉿kali)-[~/…/Matryoshka_doll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted]
└─$ ls
2DD3B.zip  base_images

┌──(kali㉿kali)-[~/…/Matryoshka_doll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted]
└─$ cd base_images       

┌──(kali㉿kali)-[~/…/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images]
└─$ ls
3_c.jpg

┌──(kali㉿kali)-[~/…/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images]
└─$ binwalk -e 3_c.jpg   

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 428 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
123606        0x1E2D6         Zip archive data, at least v2.0 to extract, compressed size: 77651, uncompressed size: 79809, name: base_images/4_c.jpg
201423        0x312CF         End of Zip archive, footer length: 22

┌──(kali㉿kali)-[~/…/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images]
└─$ ls
3_c.jpg  _3_c.jpg.extracted

┌──(kali㉿kali)-[~/…/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images]
└─$ cd _3_c.jpg.extracted 

┌──(kali㉿kali)-[~/…/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted]
└─$ cd base_images       

┌──(kali㉿kali)-[~/…/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images]
└─$ ls
4_c.jpg

┌──(kali㉿kali)-[~/…/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images]
└─$ open 4_c.jpg 

┌──(kali㉿kali)-[~/…/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images]
└─$ strings 4_c.jpg | grep picoCTF

┌──(kali㉿kali)-[~/…/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images]
└─$ binwalk -e 4_c.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 320 x 768, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
79578         0x136DA         Zip archive data, at least v2.0 to extract, compressed size: 65, uncompressed size: 81, name: flag.txt
79787         0x137AB         End of Zip archive, footer length: 22

┌──(kali㉿kali)-[~/…/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images]
└─$ ls
4_c.jpg  _4_c.jpg.extracted

┌──(kali㉿kali)-[~/…/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images]
└─$ cd _4_c.jpg.extracted 

┌──(kali㉿kali)-[~/…/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted]
└─$ ls
136DA.zip  flag.txt

┌──(kali㉿kali)-[~/…/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted]
└─$ cat flag.txt         
picoCTF{4f11048e83ffc7d342a15bd2309b47de}  

┌──(kali㉿kali)-[~/…/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted]
└─$
```

### Flag: picoCTF{4f11048e83ffc7d342a15bd2309b47de}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| binwalk | Binwalk es una herramienta rápida y fácil de usar para analizar, realizar ingeniería inversa y extraer imágenes de firmware. |

## Referencias:
- https://es.wikipedia.org/wiki/Matrioshka