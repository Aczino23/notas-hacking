# miniRSA

## Descripción: 
Let's decrypt this: [ciphertext](https://jupiter.challenges.picoctf.org/static/ee7e2388b45f521b285334abb5a63771/ciphertext)? Something seems a bit small.

**Pistas:**
1. RSA [tutorial](https://en.wikipedia.org/wiki/RSA_(cryptosystem))
2. How could having too small an e affect the security of this 2048 bit key?
3. Make sure you don't lose precision, the numbers are pretty big (besides the e value)

## Solución:
1. Pare este retos e nos proporciona un archivo con lo siguiente: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/miniRSA]
└─$ ls
ciphertext

┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/miniRSA]
└─$ cat ciphertext 
N: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e: 3
ciphertext (c): 2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125                                                                                                                           
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/miniRSA]
└─$
```

2. En RSA, `M^3 mod n = c`. Esto también se puede escribir como `M^3 = tn + c` para algún `t`. Entonces, esto significa que `M = iroot(tn+c, 3)`. Solo necesitamos encontrar la `t` correcta. Dado que `(M^3)` es solo "apenas" mayor que n, no debería llevar mucho tiempo:

```python
import gmpy2

n = 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673

e = 3

c = 2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125

for i in range(10000):
    m, is_true_root = gmpy2.iroot(i*n + c, e)
    if is_true_root:
        print(f"Found i = {i}")
        print("Message: {}".format(bytearray.fromhex(format(m, 'x')).decode()))
        break
```


```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/miniRSA]
└─$ python3 exp.py   
Found i = 0
Message: picoCTF{n33d_a_lArg3r_e_606ce004}
                                                                                
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/miniRSA]
└─$
```

### Flag: picoCTF{n33d_a_lArg3r_e_606ce004}

## Notas adicionales:

## RSA

El algoritmo de clave pública RSA fuecreado en 1978 por Rivest, Shamir y Adlman, y es el sistema criptográfico asimétrico más conocido y usado. Estos señores se basaron en el artículo de Diffie-Hellman sobre sistemas de llave pública, crearon su algoritmo y fundaron la empresa RSA Data Security Inc., que es actualmente una de las más prestigiosas en el entorno de la protección de datos.

El sistema RSA se basa en el hecho matemático de la dificultad de factorizar números muy grandes. Para factorizar un número el sistema más lógico consiste en empezar a dividir sucesivamente éste entre 2, entre 3, entre 4,..., y así sucesivamente, buscando que el resultado de la división sea exacto, es decir, de resto 0, con lo que ya tendremos un divisor del número.

Ahora bien, si el número considerado es un número primo (el que sólo es divisible por 1 y por él mismo), tendremos que para factorizarlo habría que empezar por 1, 2, 3,........... hasta llegar a él mismo, ya que por ser primo ninguno de los números anteriores es divisor suyo. Y si el número primo es lo suficientemente grande, el proceso de factorización es complicado y lleva mucho tiempo.

## Referencias:
- https://simple.wikipedia.org/wiki/RSA_algorithm