## Objetivo:
To get truly 1337, you must understand different data encodings, such as hexadecimal or binary. Can you get the flag from this program to prove you are on the way to becoming 1337? Connect with `nc jupiter.challenges.picoctf.org 15130`.

**Hints:** 
1. I hear python can convert things.
2. It might help to have multiple windows open.

## Solución:
En este reto se tienen que hace diferentes codificaciones en diferentes bases como:
- De Binario a ASCII
- De Ocatal a ASCII
- De Hexadecimal a ASCII

para esto utilizamos la herramienta  [**CyberChef**](https://gchq.github.io/CyberChef/) .

```bash
┌──(kali㉿kali)-[~]
└─$ nc jupiter.challenges.picoctf.org 15130
Let us see how data is stored
computer
Please give the 01100011 01101111 01101101 01110000 01110101 01110100 01100101 01110010 as a word.
...
you have 45 seconds.....

Input:
computer
Please give me the  163 165 142 155 141 162 151 156 145 as a word.
Input:
submarine
Please give me the 6368616972 as a word.
Input:
chair
You've beaten the challenge
Flag: picoCTF{learning_about_converting_values_02167de8}
                                                                                          
┌──(kali㉿kali)-[~]
└─$ 
```

**flag:** picoCTF{learning_about_converting_values_02167de8}

## Notas adicionales:

- **Codificación binario a texto** es un tipo de _[codificación](https://es.wikipedia.org/wiki/Codificaci%C3%B3n_de_caracteres "Codificación de caracteres") de transporte de datos_ , que tiene la finalidad de proteger los datos que se envían a otros ordenadores y evitar así daños debido a ciertas restricciones de la capa de la red de transmisión que es la responsable del transporte de los datos

- El **sistema octal** es el [sistema de numeración](https://es.wikipedia.org/wiki/Sistema_de_numeraci%C3%B3n "Sistema de numeración") posicional cuya base es igual [8](https://es.wikipedia.org/wiki/Ocho "Ocho"), utilizando los dígitos indio arábigos: 0, 1, 2, 3, 4, 5, 6, 7 y 8. En [informática](https://es.wikipedia.org/wiki/Inform%C3%A1tica "Informática") a veces se utiliza la numeración octal en vez de la [hexadecimal](https://es.wikipedia.org/wiki/Sistema_hexadecimal "Sistema hexadecimal"). Tiene la ventaja de que no requiere utilizar otros símbolos diferentes de los dígitos.

- El **sistema hexadecimal** (abreviado **hex.**) es el [sistema de numeración posicional](https://es.wikipedia.org/wiki/Sistema_de_numeraci%C3%B3n_posicional "Sistema de numeración posicional") que tiene como base el 16. Su uso actual está muy vinculado a la [informática](https://es.wikipedia.org/wiki/Inform%C3%A1tica "Informática") y [ciencias de la computación](https://es.wikipedia.org/wiki/Ciencias_de_la_computaci%C3%B3n "Ciencias de la computación") donde las operaciones de la [CPU](https://es.wikipedia.org/wiki/Unidad_central_de_procesamiento "Unidad central de procesamiento") suelen usar el [byte](https://es.wikipedia.org/wiki/Byte "Byte") u octeto como unidad básica de [memoria](https://es.wikipedia.org/wiki/Memoria_(inform%C3%A1tica) "Memoria (informática)"), debido a que un byte representa 28![2^{8}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b061b2d259bfa20a0ca0f7bb679f4cc366aacdd0) valores posibles, y esto puede representarse como 28=24⋅24=16⋅16=![2^{8}=2^{4}\cdot 2^{4}=16\cdot 16=](https://wikimedia.org/api/rest_v1/media/math/render/svg/b9ae0da27bb2a4fe27a014f2988966c6bfa43a6e) 1⋅162+0⋅161+0⋅160![1\cdot 16^{2}+0\cdot 16^{1}+0\cdot 16^{0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f795644bd7fc81bebfd138d3774ca7d95471d2a5), que equivale al número en base 16 10016![100_{{16}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3b7c8020769b29998537f4ec620a1783507525e5); dos dígitos hexadecimales corresponden exactamente a un byte.

## Referencias:
- https://www.rapidtables.com/convert/number/binary-to-ascii.html
- https://onlineasciitools.com/convert-octal-to-ascii