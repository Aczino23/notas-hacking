## Objetivo:
Can you crack the password to get the flag?Download the password checker [here](https://artifacts.picoctf.net/c/18/level2.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/18/level2.flag.txt.enc) in the same directory too.

**Hints:**
1. Does that encoding look familiar?
2. The `str_xor` function does not need to be reverse engineered for this challenge.

## Solución:
Para este reto se nos dan dos archivos uno que contiene la bandera encriptada y el otro es un script de Python:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_2]
└─$ ls
level2.flag.txt.enc  level2.py

┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_2]
└─$ cat level2.flag.txt.enc 
CP
pm%GKWP[fVT]^R
              TfVU\Q\                                                                                                                                                             
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_2]
└─$ 
```

Al momento de correr el script vemos que nos pide una contraseña:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_2]
└─$ python3 level2.py
Please enter correct password for flag: hola
That password is incorrect

┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_2]
└─$ 
```

Al parece este script se encarga de desencriptar la bandera. Cuándo revisamos el código de dicho script vemos que existe una validación de contraseña:

```python
### THIS FUNCTION WILL NOT HELP YOU FIND THE FLAG --LT ########################
def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)        
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])
###############################################################################

flag_enc = open('level2.flag.txt.enc', 'rb').read()



def level_2_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    if( user_pw == chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65) ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")



level_2_pw_check()
```

En el código del script observamos que la contraseña esta dada por la concatenación de: `chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65)`, por lo con el interprete de Python podemos obtener la contraseña:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_2]
└─$ python3          
Python 3.10.9 (main, Dec  7 2022, 13:47:07) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print(chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65))
39ce
>>>
```

Una vez que obtenemos la contraseña corremos el script nuevamente y obtenemos la bandera del reto:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_2]
└─$ python3 level2.py 
Please enter correct password for flag: 39ce
Welcome back... your flag, user:
picoCTF{tr45h_51ng1ng_502ec42e}

┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_2]
└─$ 
```

### Flag: picoCTF{tr45h_51ng1ng_502ec42e}

## Notas adicionales:

### Función `chr` de Python: 
Devuelve una cadena de un carácter cuyo código ASCII es el número especificado.

**Sintaxis:**
**chr** _(number)_

_number_

Required. Any integer within the 0-255 range.

**Valor de retorno:** str

**Ejemplo:**

```bash
>>> chr(65)
'A'
>>> chr(97)
'a'
>>> ''.join([chr(c) for c in range(65, 91)])
'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
```

## Referencias:
- https://python-reference.readthedocs.io/en/latest/docs/functions/chr.html
