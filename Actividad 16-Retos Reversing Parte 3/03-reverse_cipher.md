# reverse_cipher

## Descripción: 
We have recovered a [binary](https://jupiter.challenges.picoctf.org/static/7aa5f383ec616fe9d72c2ffe1fabd0d9/rev) and a [text file](https://jupiter.challenges.picoctf.org/static/7aa5f383ec616fe9d72c2ffe1fabd0d9/rev_this). Can you reverse the flag.

**Pistas:**
1. objdump and Gihdra are some tools that could assist with this.

## Solución:
1. Para este reto se nos dan dos archivos al parecer uno de ellos es un ejecutable y el otro un archivo de texto: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/reverse_cipher]
└─$ ls        
rev  rev_this

┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/reverse_cipher]
└─$ file *    
rev:      ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=523d51973c11197605c76f84d4afb0fe9e59338c, not stripped
rev_this: ASCII text, with no line terminators

┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/reverse_cipher]
└─$ cat rev_this 
picoCTF{w1{1wq84fb<1>49}                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/reverse_cipher]
└─$ 
```

2. Con un pequeño script en Python realizamos la ingeniería inversa a la bandera: 

```python
flag = ""

with open("rev_this", "rb") as data:
    for i in range(8):
        flag += chr(data.read(1)[0])
    for i in range(8, 23):
        if (i & 1) == 0:
            flag += chr(data.read(1)[0] - 5)
        else:
            flag += chr(data.read(1)[0] + 2)
    flag+= chr(data.read(1)[0])

print("Flag: {}".format(flag))
```

3. Obtenemos la bandera con el script anterior: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/reverse_cipher]
└─$ python3 exp.py
Flag: picoCTF{r3v3rs36ad73964}
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/reverse_cipher]
└─$ 
```

### Flag: picoCTF{r3v3rs36ad73964}

## Notas adicionales:

## Referencias: