## Objetivo:
What does this `bDNhcm5fdGgzX3IwcDM1` mean? I think it has something to do with bases.

**Hints:** Submit your answer in our flag format. For example, if your answer was 'hello', you would submit 'picoCTF{hello}' as the flag.

## Solución:
Usando la herramienta [**CyberChef**](https://gchq.github.io/CyberChef/) nos damos cuenta que la cadena esta codificada en base 64, por lo que al momento de descodificar la cadena obtenemos la flag.  

**flag:** picoCTF{l3arn_th3_r0p35}

## Notas adicionales:

### Base 64:
**Base64** es un sistema de numeración "Sistema de numeración") posicional que usa 64 como base. Es la mayor potencia que puede ser representada usando únicamente los caracteres imprimibles de ASCII. Esto ha propiciado su uso para codificación de correos electrónicos, PGP y otras aplicaciones. Todas las variantes famosas que se conocen con el nombre de Base64 usan el rango de caracteres A-Z, a-z y 0-9 en este orden para los primeros 62 dígitos, pero los símbolos escogidos para los últimos dos dígitos varían considerablemente de unas a otras. Otros métodos de codificación como UUEncode y las últimas versiones de binhex usan un conjunto diferente de 64 caracteres para representar 6 dígitos binarios, pero estos nunca son llamados Base64.

## Referencias:
- https://gchq.github.io/CyberChef/
- https://es.wikipedia.org/wiki/Base64