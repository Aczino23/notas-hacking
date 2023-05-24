# transposition-trial

## Descripción: 
Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message.Download the corrupted message [here](https://artifacts.picoctf.net/c/191/message.txt).

**Pistas:**
1. Split the message up into blocks of 3 and see how the first block is scrambled

## Solución:
1. En este reto se nos da un archivo con el siguiente contenido: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/transposition-trial]
└─$ ls
message.txt
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/transposition-trial]
└─$ cat message.txt       
heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V6E5926A}4                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/transposition-trial]
└─$
```

2. Como nos dice la descripción, en un grupo de 3 caracteres (incluyendo el espacio), se pondrá el ultimo char al principio y se recorrerán los primeros dos un espacio. Lo explico de la siguiente forma:

```txt
c0 = "heTfl g as iicpCTo" #Texto original
c1 = "heT|fl |g a|s i|icp|CTo" #Lo dividimos en grupos
c2= "The| fl|ag |is |pic|oCT" #Se cambia el orden
```

3. Para cambiarlo de una manera fácil, cree el siguiente script en Python:

```python
c = "heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V6E5926A}4"

cList = list(c)
nList = []
flag = ""

for i, char in enumerate(cList):
    if ((i + 1) % 3 == 0):
        nList.append(cList[i])
        nList.append(cList[i-2])
        nList.append(cList[i-1])
 
for char in nList:
    flag += char

print(flag)
```

4. Y así obtenemos la flag: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/transposition-trial]
└─$ python3 exp.py
The flag is picoCTF{7R4N5P051N6_15_3XP3N51V3_56E6924A}
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/transposition-trial]
└─$ 

```

### Flag: picoCTF{7R4N5P051N6_15_3XP3N51V3_56E6924A

## Notas adicionales:

## Referencias: