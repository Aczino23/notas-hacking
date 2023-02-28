## Objetivo:
Can you find the flag in [file](https://jupiter.challenges.picoctf.org/static/315d3325dc668ab7f1af9194f2de7e7a/file)? This would be really tedious to look through manually, something tells me there is a better way.

**Hints:** grep [tutorial](https://ryanstutorials.net/linuxtutorial/grep.php)

## Solución:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/frist_grep]
└─$ cat file | grep picoCTF
picoCTF{grep_is_good_to_find_things_f77e0797}
                                                                                          
┌──(kali㉿kali)-[~/picoCTF/generalSkills/frist_grep]
└─$ 
```

**flag:** picoCTF{grep_is_good_to_find_things_f77e0797}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| grep | Es una herramienta de línea de comando usada en sistemas Linux y Unix para buscar un patrón específico en un archivo o grupo de archivos. |

## Referencias:
- https://ryanstutorials.net/linuxtutorial/grep.php