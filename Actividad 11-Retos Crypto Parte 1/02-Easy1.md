# Easy1

## Descripción: 
The one time pad can be cryptographically secure, but not when you know the key. Can you solve this? We've given you the encrypted flag, key, and a table to help `UFJKXQZQUNB` with the key of `SOLVECRYPTO`. Can you use this [table](https://jupiter.challenges.picoctf.org/static/1fd21547c154c678d2dab145c29f1d79/table.txt) to solve it?.

**Pistas:**
1. Submit your answer in our flag format. For example, if your answer was 'hello', you would submit 'picoCTF{HELLO}' as the flag.
2. Please use all caps for the message.

```txt
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 
   +----------------------------------------------------
A | A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
B | B C D E F G H I J K L M N O P Q R S T U V W X Y Z A
C | C D E F G H I J K L M N O P Q R S T U V W X Y Z A B
D | D E F G H I J K L M N O P Q R S T U V W X Y Z A B C
E | E F G H I J K L M N O P Q R S T U V W X Y Z A B C D
F | F G H I J K L M N O P Q R S T U V W X Y Z A B C D E
G | G H I J K L M N O P Q R S T U V W X Y Z A B C D E F
H | H I J K L M N O P Q R S T U V W X Y Z A B C D E F G
I | I J K L M N O P Q R S T U V W X Y Z A B C D E F G H
J | J K L M N O P Q R S T U V W X Y Z A B C D E F G H I
K | K L M N O P Q R S T U V W X Y Z A B C D E F G H I J
L | L M N O P Q R S T U V W X Y Z A B C D E F G H I J K
M | M N O P Q R S T U V W X Y Z A B C D E F G H I J K L
N | N O P Q R S T U V W X Y Z A B C D E F G H I J K L M
O | O P Q R S T U V W X Y Z A B C D E F G H I J K L M N
P | P Q R S T U V W X Y Z A B C D E F G H I J K L M N O
Q | Q R S T U V W X Y Z A B C D E F G H I J K L M N O P
R | R S T U V W X Y Z A B C D E F G H I J K L M N O P Q
S | S T U V W X Y Z A B C D E F G H I J K L M N O P Q R
T | T U V W X Y Z A B C D E F G H I J K L M N O P Q R S
U | U V W X Y Z A B C D E F G H I J K L M N O P Q R S T
V | V W X Y Z A B C D E F G H I J K L M N O P Q R S T U
W | W X Y Z A B C D E F G H I J K L M N O P Q R S T U V
X | X Y Z A B C D E F G H I J K L M N O P Q R S T U V W
Y | Y Z A B C D E F G H I J K L M N O P Q R S T U V W X
Z | Z A B C D E F G H I J K L M N O P Q R S T U V W X Y
```

## Solución:
1. Este es un cifrado [Vigenère clásico](https://www.dcode.fr/vigenere-cipher). Es fácilmente solucionable usando cualquier decodificador en línea, como [Cyberchef](https://gchq.github.io/CyberChef/).

2. Para decodificar el mensaje manualmente, utilizamos el siguiente algoritmo:
	1. Para cada letra de la clave:
		1. Encuentra la fila correspondiente a la letra.
		2. En la fila, busque la columna que contiene la letra del texto cifrado coincidente
		3. La letra de texto sin formato correspondiente se anota en la parte superior de la columna.
En nuestro caso, el texto sin formato es CRYPTOISFUN.

3. Script en Python para realizar la descodificación: 

```python
alfabeto =  "ABCDEFGHIJKLMNOPQRSTUVWXYZ"

key =  "SOLVECRYPTO"

encrypted_flag =  "UFJKXQZQUNB"

len_text =  len(encrypted_flag)

for i in range(len_text):
    if((ord(encrypted_flag[i])-ord(key[i]))>=0):
        print(chr(ord(encrypted_flag[i])-ord(key[i])+65), end = '')
    else:
        print(chr(ord(encrypted_flag[i])-ord(key[i])+91), end = '')
```

### Flag: picoCTF{CRYPTOISFUN}

## Notas adicionales:

### **El cifrado de Vigenère**:
El cifrado Vigenère es un cifrado basado en diferentes series de caracteres o letras del cifrado César formando estos caracteres una tabla, llamada tabla de Vigenère, que se usa como clave. El cifrado de Vigenère es un cifrado polialfabético y de sustitución.

## Referencias:
- https://www.dcode.fr/vigenere-cipher
- https://es.wikipedia.org/wiki/Cifrado_de_Vigen%C3%A8re