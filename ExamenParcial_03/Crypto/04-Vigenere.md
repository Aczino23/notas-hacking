# Vigenere

## Descripción: 
Can you decrypt this message?Decrypt this [message](https://artifacts.picoctf.net/c/160/cipher.txt) using this key "CYLAB".

**Pistas:**
1. https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher

## Solución:
1. En este reto se nos da un archivo con el siguiente contenido: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/Vigenere]
└─$ ls
cipher.txt
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/Vigenere]
└─$ cat cipher.txt 
rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_2951c89f}
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/cryptography/Vigenere]
└─$ 
```

2. Como dice el titulo, este reto se trata de `Encripción Vigenere`. Por lo que usando el decodificador online [Vigenere Cipher](https://www.dcode.fr/vigenere-cipher) pude desencriptar fácilmente el mensaje utilizando la clave proporcionada y obtenemos la flag:

### Flag: picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_2951a89h}

## Notas adicionales:

### **El cifrado de Vigenère**:
El cifrado Vigenère es un cifrado basado en diferentes series de caracteres o letras del cifrado César formando estos caracteres una tabla, llamada tabla de Vigenère, que se usa como clave. El cifrado de Vigenère es un cifrado polialfabético y de sustitución.

## Referencias:
- https://www.dcode.fr/vigenere-cipher