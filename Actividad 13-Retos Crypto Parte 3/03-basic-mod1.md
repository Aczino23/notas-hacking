# basic-mod1

## Descripción: 
We found this weird message being passed around on the servers, we think we have a working decryption scheme.Download the message [here](https://artifacts.picoctf.net/c/128/message.txt).Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.Wrap your decrypted message in the picoCTF flag format (i.e. `picoCTF{decrypted_message}`)

**Pistas:**
1. Do you know what `mod 37` means?
2. `mod 37` means modulo 37. It gives the remainder of a number after being divided by 37.

## Solución:
1. En este reto se nos da un archivo con el siguiente mensaje: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/basic-mod1]
└─$ ls
message.txt
                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/basic-mod1]
└─$ cat message.txt 
165 248 94 346 299 73 198 221 313 137 205 87 336 110 186 69 223 213 216 216 177 138                                                                                        
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/basic-mod1]
└─$
```

2.  Según la descripción, tenemos que seguir las siguientes reglas:

```txt
A: 0
B: 1
C: 2
D: 3
E: 4
F: 5
G: 6
H: 7
I: 8
J: 9
K: 10
L: 11
M: 12
N: 13
O: 14
P: 15
Q: 16
R: 17
S: 18
T: 19
U: 20
V: 21
W: 22
X: 23
Y: 24
Z: 25
0: 26
1: 27
2: 28
3: 29
4: 30
5: 31
6: 32
7: 33
8: 34
9: 35
_: 36
```

3. Después tenemos que encontrar el modulo 37 de los siguientes valores:

```txt
165 248 94 346 299 73 198 221 313 137 205 87 336 110 186 69 223 213 216 216 177 138
```

4.  Para obtener la flag de manera fácil usamos el siguiente script en Python:

```python
datos = open('message.txt').read().split()

print(datos)

flag = ''

for n in datos:
        c = int(n) % 37
        if c >= 0 and c <= 25:
                s = chr(c+65)
        elif c >= 26 and c <= 35:
                s = chr(c+22)
        else:
                s = '_'
        flag += s

print(flag)
```

5. Lo que nos da como salida lo siguinte: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/basic-mod1]
└─$ python3 exp2.py
['165', '248', '94', '346', '299', '73', '198', '221', '313', '137', '205', '87', '336', '110', '186', '69', '223', '213', '216', '216', '177', '138']
R0UND_N_R0UND_B6B25531
                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/basic-mod1]
└─$ 
```

### Flag: picoCTF{R0UND_N_R0UND_B6B25531}

## Notas adicionales:

## Referencias: