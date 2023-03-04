## Objetivo:
Can you look at the data in this binary: [static](https://mercury.picoctf.net/static/0f6ea599582dcce7b4f1ba94e3617baf/static)? This [BASH script](https://mercury.picoctf.net/static/0f6ea599582dcce7b4f1ba94e3617baf/ltdis.sh) might help!

**Hints:**

## Solución:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/static_aint_always_noise]
└─$ ls
static
                                                                                   
┌──(kali㉿kali)-[~/picoCTF/generalSkills/static_aint_always_noise]
└─$ strings static | grep picoCTF
picoCTF{d15a5m_t34s3r_6f8c8200}
                                                                                   
┌──(kali㉿kali)-[~/picoCTF/generalSkills/static_aint_always_noise]
└─$
```

### **flag:** picoCTF{d15a5m_t34s3r_6f8c8200}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| strings | Muestra las cadenas de caracteres imprimibles que contengan los ficheros, útil para visualizar ficheros que no sean, o que no se sepa que son de texto plano. | 

## Referencias:
- https://howtoforge.es/tutorial-de-comandos-de-cadenas-de-linux-para-principiantes-5-ejemplos/