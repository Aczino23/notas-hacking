## Objetivo:
If I told you a word started with 0x70 in hexadecimal, what would it start with in ASCII?

**Hints:** Submit your answer in our flag format. For example, if your answer was 'hello', you would submit 'picoCTF{hello}' as the flag.

## Solución:

```bash
┌──(kali㉿kali)-[~]
└─$ printf '\x70' 
p                                                                                   
┌──(kali㉿kali)-[~]
└─$ 
```

**flag**: picoCTF{p}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| printf | El comando printf formatea e imprime los datos en la consola. Podemos usar este comando para convertir un carácter de hexadecimal a ASCII: |

## Referencias:
- https://es.wikipedia.org/wiki/ASCII
- https://www.baeldung.com/linux/character-hex-to-ascii