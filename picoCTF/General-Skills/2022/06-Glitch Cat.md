## Objetivo:
Our flag printing service has started glitching!`$ nc saturn.picoctf.net 51109`

**Hints:**
1. ASCII is one of the most common encodings used in programming
2. We know that the glitch output is valid Python, somehow!
3. Press Ctrl and c on your keyboard to close your connection and return to the command prompt.

## Solución:
En este reto se nos pide conectarnos a un servidor usando `netcat` , pero cuando nos conectamos el servidor nos responde con un mensaje un poco raro. Al parecer este mensaje es la bandera.
1. Para poder descifrar la bandera usamos Python ya que la función `chr` devuelve una cadena de un carácter cuyo código ASCII es el número especificado:

```bash
┌──(kali㉿kali)-[~]
└─$ nc saturn.picoctf.net 51109
'picoCTF{gl17ch_m3_n07_' + chr(0x62) + chr(0x64) + chr(0x61) + chr(0x36) + chr(0x38) + chr(0x66) + chr(0x37) + chr(0x35) + '}'

┌──(kali㉿kali)-[~]
└─$ python3          
Python 3.10.9 (main, Dec  7 2022, 13:47:07) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print('picoCTF{gl17ch_m3_n07_' + chr(0x62) + chr(0x64) + chr(0x61) + chr(0x36) + chr(0x38) + chr(0x66) + chr(0x37) + chr(0x35) + '}')
picoCTF{gl17ch_m3_n07_bda68f75}
>>>
```

### Flag: picoCTF{gl17ch_m3_n07_bda68f75}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| nc | Es un comando que permite acceder a puertos TCP o UDP de la propia máquina o de otras máquinas remotas. También permite quedar a la escucha en un puerto dado (TCP o UDP) de la máquina local. | 

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