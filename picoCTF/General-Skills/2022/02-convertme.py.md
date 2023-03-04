## Objetivo:
Run the Python script and convert the given number from decimal to binary to get the flag.[Download Python script](https://artifacts.picoctf.net/c/31/convertme.py)

**Hints:**
1. Look up a decimal to binary number conversion app on the web or use your computer's calculator!
2. The `str_xor` function does not need to be reverse engineered for this challenge.
3. If you have Python on your computer, you can download the script normally and run it. Otherwise, use the `wget` command in the webshell.
4. To use `wget` in the webshell, first right click on the download link and select 'Copy Link' or 'Copy Link Address'
5. Type everything after the dollar sign in the webshell: `$ wget` , then paste the link after the space after `wget` and press enter. This will download the script for you in the webshell so you can run it!
6. Finally, to run the script, type everything after the dollar sign and then press enter: `$ python3 convertme.py`

## Solución:
En este reto se nos pide ejecutar un script de Python, dicho script nos indica que debemos realizar una conversión de un numero decimal a binario.
Para realizar la conversion de decimal a binario usamnos la sigunte pagina: [RapidTables](https://www.rapidtables.com/convert/number/decimal-to-binary.html) 

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/convertme.py]
└─$ ls
convertme.py
                                                                                        
┌──(kali㉿kali)-[~/picoCTF/generalSkills/convertme.py]
└─$ python3 convertme.py
If 24 is in decimal base, what is it in binary base?
Answer: 11000
That is correct! Here's your flag: picoCTF{4ll_y0ur_b4535_9c3b7d4d}
                                                
┌──(kali㉿kali)-[~/picoCTF/generalSkills/convertme.py]
└─$
```

### **flag:** picoCTF{4ll_y0ur_b4535_9c3b7d4d}

## Notas adicionales:

### Python: 
Python es un poderoso lenguaje de programación de código abierto, creado por Guido van Rossum en 1991. Python se diseñó como un lenguaje de programación interpretado para el uso general. «Lenguaje interpretado» significa que el código de programación se convierte en bytecode y luego se ejecuta por el interpretador, que en este caso es la máquina virtual de Python.

## Referencias:
- https://www.discoduroderoer.es/ejecutar-python-en-consola-en-linux/
- https://www.rapidtables.com/convert/number/decimal-to-binary.html