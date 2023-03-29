## Descripción: 
I stopped using YellowPages and moved onto WhitePages... but [the page they gave me](https://jupiter.challenges.picoctf.org/static/fa4a277cfa846e07a5981d8a19288a2e/whitepages.txt) is all blank!

**Pistas:**

## Solución:
1. En este reto se los da un archivo de texto que al parecer no contiene nada mas que espacios en blanco: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/WhitePages]
└─$ ls
whitepages.txt

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/WhitePages]
└─$ cat whitepages.txt                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/WhitePages]
└─$ 
```

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/WhitePages]
└─$ file whitepages.txt 
whitepages.txt: Unicode text, UTF-8 text, with very long lines (1376), with no line terminators

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/WhitePages]
└─$ xxd whitepages.txt| head
00000000: e280 83e2 8083 e280 83e2 8083 20e2 8083  ............ ...
00000010: 20e2 8083 e280 83e2 8083 e280 83e2 8083   ...............
00000020: 20e2 8083 e280 8320 e280 83e2 8083 e280   ...... ........
00000030: 83e2 8083 20e2 8083 e280 8320 e280 8320  .... ...... ... 
00000040: 2020 e280 83e2 8083 e280 83e2 8083 e280    ..............
00000050: 8320 20e2 8083 20e2 8083 e280 8320 e280  .  ... ...... ..
00000060: 8320 20e2 8083 e280 83e2 8083 2020 e280  .  .........  ..
00000070: 8320 20e2 8083 2020 2020 e280 8320 e280  .  ...    ... ..
00000080: 83e2 8083 e280 83e2 8083 2020 e280 8320  ..........  ... 
00000090: e280 8320 e280 8320 e280 83e2 8083 e280  ... ... ........

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/WhitePages]
└─$
```

2. Con un pequeño  script de Python remplazamos los espacios en blanco  (Unicode) para obtener la flag:  

```python
from pwn import *

with open('whitepages.txt', 'rb') as f:
    data = f.read() 

data = data.replace(b'\xe2\x80\x83', b'0').replace(b' ', b'1')

data = data.decode("ascii")

print(unbits(data).decode("ascii")) 
```

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/WhitePages]
└─$ python script.py

        picoCTF

        SEE PUBLIC RECORDS & BACKGROUND REPORT
        5000 Forbes Ave, Pittsburgh, PA 15213
        picoCTF{not_all_spaces_are_created_equal_3e2423081df9adab2a9d96afda4cfad6}
                                                                                                
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/WhitePages]
└─$
```


### Flag: picoCTF{not_all_spaces_are_created_equal_3e2423081df9adab2a9d96afda4cfad6}

## Notas adicionales:

### Unicode:
Unicode es un sistema de codificación de caracteres utilizado por los equipos informáticos para el almacenamiento y el intercambio de datos en formato de texto. Asigna un número único (un punto del código) a cada carácter de los principales sistemas de escritura del mundo. También incluye símbolos técnicos y de puntuación, y otros muchos caracteres utilizados en la escritura de textos.

## Referencias:
- https://en.wikipedia.org/wiki/Unicode
- https://www.compart.com/en/unicode/category/Zs
- https://en.wikipedia.org/wiki/UTF-8