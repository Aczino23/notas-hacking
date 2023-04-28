# Roboto Sans

## Descripción: 
The flag is somewhere on this web application not necessarily on the website. Find it.Check [this](http://saturn.picoctf.net:55771/) out.

**Pistas:**

## Solución:
1. Se nos proporciona el siguiente sitio web: 

![Pasted image 20230427121158](Pasted%20image%2020230427121158.png)

2. Al parecer el sitio tiene un archivo robots.txt: 

![Pasted image 20230427121310](Pasted%20image%2020230427121310.png)

3. En el archivo robots.txt encontramos una cadena que al parecer esta codificada en base 64: 

```bash
┌──(kali㉿kali)-[~]
└─$ echo "anMvbXlmaWxlLnR4dA==" | base64 -d
js/myfile.txt                                                                           
┌──(kali㉿kali)-[~]
└─$
```

4. Al ir a la ruta http://saturn.picoctf.net:55771/js/myfile.txt obtenemos la flag: 

![Pasted image 20230427123150](Pasted%20image%2020230427123150.png)

### Flag: picoCTF{Who_D03sN7_L1k5_90B0T5_22ce1f22}

## Notas adicionales:

## Referencias: