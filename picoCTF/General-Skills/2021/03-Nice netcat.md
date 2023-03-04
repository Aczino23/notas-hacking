## Objetivo:
There is a nice program that you can talk to by using this command in a shell: `$ nc mercury.picoctf.net 21135`, but it doesn't speak English...

**Hints:**
1. You can practice using netcat with this picoGym problem: [what's a netcat?](https://play.picoctf.org/practice/challenge/34)
2. You can practice reading and writing ASCII with this picoGym problem: [Let's Warm Up](https://play.picoctf.org/practice/challenge/22)

## Solución:
Al conectarnos por **netcat** al host obtenemos una serie de números:

```bash
┌──(kali㉿kali)-[~]
└─$ nc mercury.picoctf.net 21135           
112 
105 
99 
111 
67 
84 
70 
123 
103 
48 
48 
100 
95 
107 
49 
116 
116 
121 
33 
95 
110 
49 
99 
51 
95 
107 
49 
116 
116 
121 
33 
95 
97 
102 
100 
53 
102 
100 
97 
52 
125 
10                                                                  
┌──(kali㉿kali)-[~]
└─$
```

Lo que hacemos es obtener el carácter en ASCII de cada numero para así formar la flag, para realizar esto hacemos uso de la pagina [Cipher Identifier](https://www.dcode.fr/ascii-code)

### **flag:** picoCTF{g00d_k1tty!_n1c3_k1tty!_afd5fda4}

## Notas adicionales:
- **ASCII** ([acrónimo](https://es.wikipedia.org/wiki/Acr%C3%B3nimo "Acrónimo") [inglés](https://es.wikipedia.org/wiki/Idioma_ingl%C3%A9s "Idioma inglés") de _American Standard Code for Information Interchange_ —Código Estándar estadounidense para el Intercambio de Información—), pronunciado generalmente [áski][1](https://es.wikipedia.org/wiki/ASCII#cite_note-Mackenzie_1980-1)​: 6  o (rara vez) [ásθi] o [ási], es un [código de caracteres](https://es.wikipedia.org/wiki/Codificaci%C3%B3n_de_caracteres "Codificación de caracteres") basado en el [alfabeto latino](https://es.wikipedia.org/wiki/Alfabeto_latino "Alfabeto latino"), tal como se usa en inglés moderno. Fue creado en 1963 por el Comité Estadounidense de Estándares (ASA, conocido desde 1969 como el Instituto Estadounidense de Estándares Nacionales, o [ANSI](https://es.wikipedia.org/wiki/Instituto_Nacional_Estadounidense_de_Est%C3%A1ndares "Instituto Nacional Estadounidense de Estándares")) como una evolución de los conjuntos de códigos utilizados entonces en [telegrafía](https://es.wikipedia.org/wiki/Telegraf%C3%ADa "Telegrafía"). Más tarde, en 1967, se incluyeron las minúsculas, y se redefinieron algunos códigos de control para formar el código conocido como **US-ASCII.**

- El código ASCII utiliza 7 bits para representar los caracteres, aunque inicialmente empleaba un bit adicional ([bit de paridad](https://es.wikipedia.org/wiki/Bit_de_paridad "Bit de paridad")) que se usaba para detectar errores en la transmisión. A menudo se llama incorrectamente ASCII a varios [códigos de caracteres de 8 bits](https://es.wikipedia.org/wiki/C%C3%B3digo_de_caracteres_de_8_bits "Código de caracteres de 8 bits") que extienden el ASCII con caracteres propios de idiomas distintos al inglés, como el estándar [ISO/IEC 8859-1](https://es.wikipedia.org/wiki/ISO/IEC_8859-1 "ISO/IEC 8859-1").[1](https://es.wikipedia.org/wiki/ASCII#cite_note-Mackenzie_1980-1)​

## Referencias:
- https://www.dcode.fr/ascii-code
- https://elcodigoascii.com.ar/