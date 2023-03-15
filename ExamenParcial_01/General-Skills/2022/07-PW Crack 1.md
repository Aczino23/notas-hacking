## Objetivo:
Can you crack the password to get the flag?Download the password checker [here](https://artifacts.picoctf.net/c/52/level1.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/52/level1.flag.txt.enc) in the same directory too.

**Hints:**
1. To view the file in the webshell, do: `$ nano level1.py`
2. To exit `nano`, press Ctrl and x and follow the on-screen prompts.
3. The `str_xor` function does not need to be reverse engineered for this challenge.

## Solución:
Para este reto se nos dan dos archivos uno que contiene la bandera encriptada y el otro es un script de Python:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_1]
└─$ ls                     
level1.flag.txt.enc  level1.py

┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_1]
└─$ cat level1.flag.txt.enc 
A
 Rr1w▒Q nVT_nPRVW▒                                                                                            
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_1]
└─$ 
```

Al momento de correr el script vemos que nos pide una contraseña:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_1]
└─$ python3 level1.py
Please enter correct password for flag: ds
That password is incorrect

┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_1]
└─$ 
```

Al parece este script se encarga de desencriptar la bandera. Cuándo revisamos el código de dicho script vemos que existe una validación de contraseña en donde la contraseña que se ingrese debe ser `1e1a`:

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

flag_enc = open('level1.flag.txt.enc', 'rb').read()

def level_1_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    if( user_pw == "1e1a"):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")



level_1_pw_check()
```

Entonces ya teniendo la contraseña corremos el script y obtenemos la bandera:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_1]
└─$ python3 level1.py
Please enter correct password for flag: 1e1a
Welcome back... your flag, user:
picoCTF{545h_r1ng1ng_fa343060}

┌──(kali㉿kali)-[~/picoCTF/generalSkills/PW_Crack_1]
└─$
```

### Flag: picoCTF{545h_r1ng1ng_fa343060}

## Notas adicionales:


## Referencias: