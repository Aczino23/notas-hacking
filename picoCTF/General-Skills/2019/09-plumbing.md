## Objetivo:
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag? Connect to `jupiter.challenges.picoctf.org 14291`.

**Hints:**
1. Remember the flag format is picoCTF{XXXX}
2. What's a pipe? No not that kind of pipe... This [kind](http://www.linfo.org/pipes.html)

## Solución:

```bash
┌──(kali㉿kali)-[~]
└─$ nc jupiter.challenges.picoctf.org 14291 | grep picoCTF
picoCTF{digital_plumb3r_ea8bfec7}

┌──(kali㉿kali)-[~]
└─$ 
```

### **flag:** picoCTF{digital_plumb3r_ea8bfec7}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| nc | es un comando que permite acceder a puertos TCP o UDP de la propia máquina o de otras máquinas remotas. También permite quedar a la escucha en un puerto dado (TCP o UDP) de la máquina local. | 
| grep |  es una herramienta de línea de comando usada en sistemas Linux y Unix para buscar un patrón específico en un archivo o grupo de archivos.|

## Referencias:
- https://linux.die.net/man/1/nc
- https://ryanstutorials.net/linuxtutorial/grep.php