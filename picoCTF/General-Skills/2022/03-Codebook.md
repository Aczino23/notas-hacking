## Objetivo:
Run the Python script `code.py` in the same directory as `codebook.txt`.

-   [Download code.py](https://artifacts.picoctf.net/c/102/code.py)
-   [Download codebook.txt](https://artifacts.picoctf.net/c/102/codebook.txt)

**Hints:**
1. On the webshell, use `ls` to see if both files are in the directory you are in
2. The `str_xor` function does not need to be reverse engineered for this challenge.

## Solución:
Para este reto se nos pide ejecutar un script de Python, dicho programa los que realiza es descifrar la flag en base a un archivo al parcera este script desencripta la flag mediante una llave privada la cual esta contenida en el archivo `codebook.txt`

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/Codebook]
└─$ ls              
codebook.txt  code.py
                                                                                
┌──(kali㉿kali)-[~/picoCTF/generalSkills/Codebook]
└─$ python3 code.py 
picoCTF{c0d3b00k_455157_197a982c}
```

### Flag: picoCTF{c0d3b00k_455157_197a982c}

## Notas adicionales:

### Python: 
Python es un poderoso lenguaje de programación de código abierto, creado por Guido van Rossum en 1991. Python se diseñó como un lenguaje de programación interpretado para el uso general. «Lenguaje interpretado» significa que el código de programación se convierte en bytecode y luego se ejecuta por el interpretador, que en este caso es la máquina virtual de Python.

## Referencias:
- https://www.discoduroderoer.es/ejecutar-python-en-consola-en-linux/