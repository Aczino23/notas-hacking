## Objetivo:
Can you crack the password to get the flag?Download the password checker [here](https://artifacts.picoctf.net/c/23/level3.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/23/level3.flag.txt.enc) and the [hash](https://artifacts.picoctf.net/c/23/level3.hash.bin) in the same directory too.There are 7 potential passwords with 1 being correct. You can find these by examining the password checker script.

**Hints:**
1. To view the level3.hash.bin file in the webshell, do: `$ bvi level3.hash.bin`
2. To exit `bvi` type `:q` and press enter.
3. The `str_xor` function does not need to be reverse engineered for this challenge.

## Solución:
Para este reto se nos dan tres archivos uno que contiene la bandera encriptada, otro que contiene un hash y el ultimo otro es un script de Python

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_3]
└─$ ls
level3.flag.txt.enc  level3.hash.bin  level3.py

┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_3]
└─$ cat level3.flag.txt.enc 
D
RL                                                                                                                                                             
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_3]
└─$ cat level3.hash.bin    
�y�>�V ��▒�X�                                                                                                                                                             

┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_3]
└─$
```

Al momento de correr el script vemos que nos pide una contraseña:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_3]
└─$ python3 level3.py 
Please enter correct password for flag: dsjgfu
That password is incorrect

┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_3]
└─$ 
```

Al parece este script se encarga de desencriptar la bandera. Cuándo revisamos el código de dicho script vemos que existe una validación de contraseña:

```python
import hashlib

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

flag_enc = open('level3.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level3.hash.bin', 'rb').read()


def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()


def level_3_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")

level_3_pw_check()

# The strings below are 7 possibilities for the correct password. 
#   (Only 1 is correct)
pos_pw_list = ["6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"]
```

Se nos indica que existen 7 posibles contraseñas las cuales están contenidas en una lista, así que modificamos un poco el código: 

```python
import hashlib

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

flag_enc = open('level3.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level3.hash.bin', 'rb').read()


def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()


def level_3_pw_check(user_pw):
    # user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")

# The strings below are 7 possibilities for the correct password. 
#   (Only 1 is correct)
pos_pw_list = ["6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"]

for password in pos_pw_list:
        level_3_pw_check(password)
```

Una vez que modificamos el código del script volvemos a correrlo para obtener la bandera:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_3]
└─$ python3 level3.py | grep picoCTF
picoCTF{m45h_fl1ng1ng_2b072a90}

┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_3]
└─$
```

### Flag: picoCTF{m45h_fl1ng1ng_2b072a90}

## Notas adicionales:

### Recorrer una lista de Python usando el bucle `for`

Una forma sencilla de recorrer una lista o cualquier objeto iterable en Python es usando el bucle `for`. El siguiente código de ejemplo demuestra cómo usar el bucle `for` para recorrer una lista en Python.

```python
mylist = [1,4,7,3,21]

for x in mylist:
  print(x)
```

Producción:

```text
1
4
7
3
21
```

## Referencias:
- https://www.delftstack.com/es/howto/python/python-loop-through-list/