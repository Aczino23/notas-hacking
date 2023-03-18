## Objetivo:
Check the admin scratchpad! `https://jupiter.challenges.picoctf.org/problem/58210/` or http://jupiter.challenges.picoctf.org:58210

**Hints:**
1. What is that cookie?
2. Have you heard of JWT?

## Solución:
1. Vemos que se realiza una autenticación por JWT token en la pagina: 

![[img1.png]]

2. Con ayuda de de [jwt.io](https://jwt.io/introduction) descodificamos en token y vemos su contenido:

![[Pasted image 20230315140239.png]]

3. Vemos que el token tiene una firma por lo que intentamos crackearla usando la herramienta John the Ripper: 

```bash
┌──(Kali㉿kali)-[~]
└─$ john hash -w=/usr/share/wordlists/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (HMAC-SHA256 [password is key, SHA256 256/256 AVX2 8x])
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
ilovepico        (?)     
1g 0:00:00:04 DONE (2023-03-11 21:30) 0.2136g/s 1580Kp/s 1580Kc/s 1580KC/s iloverob4live345..ilovemymother@
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
                                                                            
┌──(alexia㉿kali)-[~]
└─$
```


![[Pasted image 20230315143821.png]]

4. Por ultimo enviamos el token a la página y obtenemos la flag:

![[Pasted image 20230315143922.png]]

### Flag: picoCTF{jawt_was_just_what_you_thought_44c752f5}

## Notas adicionales:

### JWT:
JSON Web Token (JWT) es un estándar abierto (RFC 7519) que define una forma compacta y autónoma de transmitir información de forma segura entre las partes como un objeto JSON. Esta información se puede verificar y confiar porque está firmada digitalmente. Los JWT se pueden firmar usando un secreto (con el algoritmo HMAC) o un par de claves pública/privada usando RSA o ECDSA.

## Referencias:
- https://jwt.io/introduction
- https://github.com/openwall/john