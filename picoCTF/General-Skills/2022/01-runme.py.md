## Objetivo:
Run the `runme.py` script to get the flag. Download the script with your browser or with `wget` in the webshell.[Download runme.py Python script](https://artifacts.picoctf.net/c/86/runme.py)

**Hints:**
1. If you have Python on your computer, you can download the script normally and run it. Otherwise, use the `wget` command in the webshell.
2. To use `wget` in the webshell, first right click on the download link and select 'Copy Link' or 'Copy Link Address'
3. Type everything after the dollar sign in the webshell: `$ wget` , then paste the link after the space after `wget` and press enter. This will download the script for you in the webshell so you can run it!
4. Finally, to run the script, type everything after the dollar sign and then press enter: `$ python3 runme.py` You should have the flag now!

## Solución:

En este retos solo se nos pide ejecutar un programa de python para obtener la flag.

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/runme.py]
└─$ ls              
runme.py
                                                                                    
┌──(kali㉿kali)-[~/picoCTF/generalSkills/runme.py]
└─$ python3 runme.py
picoCTF{run_s4n1ty_run}
                                                                                      
┌──(kali㉿kali)-[~/picoCTF/generalSkills/runme.py]
└─$
```

### **flag:** picoCTF{run_s4n1ty_run}

## Notas adicionales:

### Python: 
Python es un poderoso lenguaje de programación de código abierto, creado por Guido van Rossum en 1991. Python se diseñó como un lenguaje de programación interpretado para el uso general. «Lenguaje interpretado» significa que el código de programación se convierte en bytecode y luego se ejecuta por el interpretador, que en este caso es la máquina virtual de Python.

## Referencias:
- https://www.discoduroderoer.es/ejecutar-python-en-consola-en-linux/