## Objetivo:
Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames: [Addadshashanammu.zip](https://mercury.picoctf.net/static/9689f2b453ad5daeb73ca7534e4d1521/Addadshashanammu.zip)

**Hints:**
1. After `unzip`ing, this problem can be solved with 11 button-presses...(mostly Tab)...

## Solución:

```bash
┌──(kali㉿kali)-[~]
└─$ cd Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku 
                                                                                   
┌──(kali㉿kali)-[~/…/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku]
└─$ ls
fang-of-haynekhtnamet
                                                                                   
┌──(kali㉿kali)-[~/…/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku]
└─$ strings fang-of-haynekhtnamet | grep picoCTF 
*ZAP!* picoCTF{l3v3l_up!_t4k3_4_r35t!_2bcfb2ab}
                                                                                   
┌──(kali㉿kali)-[~/…/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku]
└─$
```

**flag:** picoCTF{l3v3l_up!_t4k3_4_r35t!_2bcfb2ab}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| unzip | Permite descomprimir **archivos zip**. | 

## Referencias:
- https://www.hostinger.mx/tutoriales/comando-unzip-linux