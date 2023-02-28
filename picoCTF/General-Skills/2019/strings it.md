## Objetivo:
Can you find the flag in [file](https://jupiter.challenges.picoctf.org/static/94d00153b0057d37da225ee79a846c62/strings) without running it?

**Hints:** [strings](https://linux.die.net/man/1/strings)

## Solución:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/strings_it]
└─$ strings strings | grep picoCTF
picoCTF{5tRIng5_1T_d66c7bb7}
                                                                                          
┌──(kali㉿kali)-[~/picoCTF/generalSkills/strings_it]
└─$ 
```

**flag:** picoCTF{5tRIng5_1T_d66c7bb7}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
|  strings | Muestra las cadenas de caracteres imprimibles que contengan los ficheros, útil para visualizar ficheros que no sean, o que no se sepa que son de texto plano. |
| grep | Es una herramienta de línea de comando usada en sistemas Linux y Unix para buscar un patrón específico en un archivo o grupo de archivos. |

## Referencias:
- https://linux.die.net/man/1/strings