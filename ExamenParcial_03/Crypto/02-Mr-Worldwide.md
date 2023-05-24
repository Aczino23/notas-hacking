# Mr-Worldwide

## Descripción: 
A musician left us a [message](https://jupiter.challenges.picoctf.org/static/d5570d48262dbba2a31f2a940409ad9d/message.txt). What's it mean?

**Pistas:**
**Sin pistas**

## Solución:
1. En este reto se nos da un archivo con el siguiente contenido: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/Mr-Worldwide]
└─$ ls
message.txt
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/Mr-Worldwide]
└─$ cat message.txt
picoCTF{(35.028309, 135.753082)(46.469391, 30.740883)(39.758949, -84.191605)(41.015137, 28.979530)(24.466667, 54.366669)(3.140853, 101.693207)_(9.005401, 38.763611)(-3.989038, -79.203560)(52.377956, 4.897070)(41.085651, -73.858467)(57.790001, -152.407227)(31.205753, 29.924526)}                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/Mr-Worldwide]
└─$
```

2. Si buscamos las coordenadas podremos encontrar ubicaciones reales, por lo que podríamos obtener la flag de la primera letra de la ubicación:

| Coordenadas | Ubicación | Letra |
| --- | --- | --- |
| (35.028309, 135.753082) | Kyoto, Japan | **K** |
| (46.469391, 30.740883) | Odessa, Ukraine | **O** |
| (39.758949, -84.191605) | Dayton, United States | **D** |
| (41.015137, 28.979530) | Istanbul, Turkey | **I** |
| (24.466667, 54.366669) | Abu Dhabi, UAE | **A** |
| (3.140853, 101.693207) | Kuala Lumpur, Malaysia | **K** |
| (9.005401, 38.763611) | Addis Ababa, Ethiopia | **A** |
| (-3.989038, -79.203560) | Loja, Ecuador | **L** |
| (52.377956, 4.897070) | Amsterdam, Netherlands | **A** |
| (41.085651, -73.858467) | Sleepy Hollow, USA | **S** |
| (57.790001, -152.407227) | Kodiak, United States | **K** |
| (31.205753, 29.924526) | Alexandria, Egypt | **A** |

3. Las letras forman el nombre de dos ubicaciones, por lo que las podríamos separar como se hace habitualmente con una flag: `KODIAK_ALASKA`. Entonces la flag es: 

### Flag: picoCTF{KODIAK_ALASKA}

## Notas adicionales:

## Referencias: