#  Lookey here

## Descripción: 
Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it.Download the data [here](https://artifacts.picoctf.net/c/126/anthem.flag.txt).

**Pistas:**
1. Download the file and search for the flag based on the known prefix. 

## Solución:
1. Para resolver este reto, se nos da el archivo `anthem.flag.txt|.

2. Como es un archivo .txt, por intuición utilizo el comando `cat`.

3. Al ver que es un texto común, utilice el comando `grep` con la palabra clave `pico`. para ver si la flag esta en el archivo. Así obtenemos la flag es:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Lookey_here]
└─$ cat anthem.flag.txt | grep picoCTF 
      we think that the men of picoCTF{gr3p_15_@w3s0m3_2116b979}
                                                                                               
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/Lookey_here]
└─$ 
```

### Flag: picoCTF{gr3p_15_@w3s0m3_2116b979}

## Notas adicionales:

## Referencias: