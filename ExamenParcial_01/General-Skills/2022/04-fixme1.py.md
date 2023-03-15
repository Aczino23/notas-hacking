## Objetivo:
Fix the syntax error in this Python script to print the flag.[Download Python script](https://artifacts.picoctf.net/c/39/fixme1.py)

**Hints:**
1. Indentation is very meaningful in Python
2. To view the file in the webshell, do: `$ nano fixme1.py`
3. To exit `nano`, press Ctrl and x and follow the on-screen prompts.
4. The `str_xor` function does not need to be reverse engineered for this challenge.

## Solución:
1. En este reto se nos pide corregir un script de Python, primero corremos el script y vemos que nos da un error:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/fixme1.py]
└─$ ls            
fixme1.py

┌──(kali㉿kali)-[~/picoCTF/generalSkills/fixme1.py]
└─$ python3 fixme1.py 
  File "/home/kali/picoCTF/generalSkills/fixme1.py/fixme1.py", line 20
    print('That is correct! Here\'s your flag: ' + flag)
IndentationError: unexpected indent

┌──(kali㉿kali)-[~/picoCTF/generalSkills/fixme1.py]
└─$ 
```

2. Al revisar el código notamos que el error se debe a la mala identación en la ultima línea del script.

```python
import random

def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)        
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])


flag_enc = chr(0x15) + chr(0x07) + chr(0x08) + chr(0x06) + chr(0x27) + chr(0x21) + chr(0x23) + chr(0x15) + chr(0x5a) + chr(0x07) + chr(0x00) + c>

  
flag = str_xor(flag_enc, 'enkidu')
print('That is correct! Here\'s your flag: ' + flag)
```

3. Una vez corregido el código ejecutamos el script y obtenemos la bandera:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/fixme1.py]
└─$ python3 fixme1.py
That is correct! Here's your flag: picoCTF{1nd3nt1ty_cr1515_182342f7}

┌──(kali㉿kali)-[~/picoCTF/generalSkills/fixme1.py]
└─$ 
```

### Flag: picoCTF{1nd3nt1ty_cr1515_182342f7}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| nano | Es un editor de texto para sistemas "Unix" basado en curses. |

### Indentación incorrecta

Mientras que la mayoría de los idiomas utilizan la sangría para mejorar su legibilidad, pero no dependen de la práctica, Python ha tejido la sangría directamente en el tejido de su idioma. Esto significa que no puede permitirse cometer errores cuando se trata de formatear su código.

Para Python, la regla es tener 4 espacios para sangrar. No mezcles con 2,3,5 o una cantidad diferente de espacios ya que Python simplemente no ejecutará tu programa.

## Referencias:
- https://stackoverflow.com/questions/1016814/what-should-i-do-with-unexpected-indent-in-python
- http://net-informations.com/python/err/indent.htm