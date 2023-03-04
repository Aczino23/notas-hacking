## Objetivo:
Fix the syntax error in the Python script to print the flag.[Download Python script](https://artifacts.picoctf.net/c/65/fixme2.py)

**Hints:**
1. Are equality and assignment the same symbol?
2. To view the file in the webshell, do: `$ nano fixme2.py`
3. To exit `nano`, press Ctrl and x and follow the on-screen prompts.
4. The `str_xor` function does not need to be reverse engineered for this challenge.

## Solución:
1. En este reto se nos pide corregir un script de Python, primero corremos el script y vemos que nos da un error:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/fixme2.py]
└─$ ls               
fixme2.py

┌──(kali㉿kali)-[~/picoCTF/generalSkills/fixme2.py]
└─$ python3 fixme2.py 
  File "/home/kali/picoCTF/generalSkills/fixme2.py/fixme2.py", line 22
    if flag = "":
       ^^^^^^^^^
SyntaxError: invalid syntax. Maybe you meant '==' or ':=' instead of '='?

┌──(kali㉿kali)-[~/picoCTF/generalSkills/fixme2.py]
└─$ 
```

2. Al revisar el tipo de error y el código nos damos cuenta que el error se encuentra en la condición `if` por lo que procedemos a corregir el error:

```python
import random

def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)        
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in
    zip(secret,new_key)])


flag_enc = chr(0x15) + chr(0x07) + chr(0x08) + chr(0x06) + chr(0x27) + chr(0x21) + chr(0x23) + chr(0x15) + chr(0x58) + chr(0x18) + chr(0x11) + c>

  
flag = str_xor(flag_enc, 'enkidu')

# Check that flag is not empty
if flag == "":
  print('String XOR encountered a problem, quitting.')
else:
  print('That is correct! Here\'s your flag: ' + flag)
```

3. Una vez corregido el código ejecutamos el script y obtenemos la bandera:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/fixme2.py]
└─$ python3 fixme2.py 
That is correct! Here's your flag: picoCTF{3qu4l1ty_n0t_4551gnm3nt_e8814d03}

┌──(kali㉿kali)-[~/picoCTF/generalSkills/fixme2.py]
└─$
```

### Flag: picoCTF{3qu4l1ty_n0t_4551gnm3nt_e8814d03}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| nano | Es un editor de texto para sistemas "Unix" basado en curses. |

### Errores de sintaxis:

Los errores de sintaxis, también conocidos como errores de interpretación, son quizás el tipo de error  más común que se tiene cuando todavía estás aprendiendo Python:

```bash
>>> while True print('Hello world')
  File "<stdin>", line 1
    while True print('Hello world')
                   ^
SyntaxError: invalid syntax
```

El intérprete reproduce la línea responsable del error y muestra una pequeña “flecha” que apunta al primer lugar donde se detectó el error. El error ha sido provocado (o al menos detectado) en el elemento que _precede_ a la flecha: en el ejemplo, el error se detecta en la función `print()`, ya que faltan dos puntos (`':'`) antes del mismo. Se muestran el nombre del archivo y el número de línea para que sepas dónde mirar en caso de que la entrada venga de un programa.

## Referencias:
- https://stackoverflow.com/questions/72424935/syntaxerror-invalid-syntax-maybe-you-meant-or-instead-of-pyth