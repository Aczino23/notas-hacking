# Mind your Ps and Qs

## Descripción: 
In RSA, a small `e` value can be problematic, but what about `N`? Can you decrypt this? [values](https://mercury.picoctf.net/static/2604f8b51a5cc62d38a3736938f19cef/values)

**Pistas:**
1. Bits are expensive, I used only a little bit over 100 to save money

## Solución:
1. Se nos dan los siguientes valores: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/Mind_your_Ps_Qs]
└─$ ls
values
                                                                                
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/Mind_your_Ps_Qs]
└─$ cat values                         
Decrypt my super sick RSA:
c: 861270243527190895777142537838333832920579264010533029282104230006461420086153423
n: 1311097532562595991877980619849724606784164430105441327897358800116889057763413423
e: 65537                                                                                
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/Mind_your_Ps_Qs]
└─$
```

2. Para poder obtener el texto plano, necesitamos de las variables `p` y `q`, para así poder obtener `tn` y después `d` y poder sustituirlos en las formula que nos da el texto plano: `m = c^d mod n`

3. Para poder obtener estas variables, utilizaremos [Factordb](http://factordb.com/) para factorizar n. Los valores que nos da son:

```bash
┌──(kali㉿kali)-[~]
└─$ python3                                             
Python 3.11.2 (main, Mar 13 2023, 12:18:29) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> p = 1955175890537890492055221842734816092141
>>> q = 670577792467509699665091201633524389157003
>>> n = p * q
>>> n
1311097532562595991877980619849724606784164430105441327897358800116889057763413423
>>>
```

3. Sabiendo esto, podemos sustituir los valores para obtener el valor de `tn` y `d` y así sustituir todas estas variables en la formula para obtener el texto plano. Para eso cree un programa en Python que nos diera la bandera sabiendo todo esto.

```bash
from Crypto.Util.number import inverse, long_to_bytes

c = 861270243527190895777142537838333832920579264010533029282104230006461420086153423
n = 1311097532562595991877980619849724606784164430105441327897358800116889057763413423
p = 1955175890537890492055221842734816092141
q = 670577792467509699665091201633524389157003
e = 65537
tn = (p-1) * (q-1)
d = inverse(e, tn)
m = pow(c, d, n)
print(long_to_bytes(m))

b'picoCTF{sma11_N_n0_g0od_13686679}'
```

### Flag: picoCTF{sma11_N_n0_g0od_13686679}

## Notas adicionales:

```txt
c - texto cifrado
m - mensaje de texto plano
p - primo 1   
q - primo 2    
n - modulo (llave publica)
tn - totient n (euler)
e - exponente (llave publica)
d - llave privada    
n = p * q
tn = (p-1) * (q-1)    
d = e mod inv tn / inverse(e, tn)

Encriptar, c = m^e mod n / pow(m, e, n)    
Desencriptar, m = c^d mod n / pow(c, d, n)
```

## Referencias:
- http://factordb.com/