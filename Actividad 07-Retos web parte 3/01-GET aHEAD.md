## Descripción: 
Find the flag being held on this server to get ahead of the competition [http://mercury.picoctf.net:34561/](http://mercury.picoctf.net:34561/)

**Pistas:**
1. Maybe you have more than 2 choices
2. Check out tools like Burpsuite to modify your requests and look at the responses

## Solución:

```bash
┌──(kali㉿kali)-[~]
└─$ curl -I HEAD http://mercury.picoctf.net:34561/index.php
curl: (6) Could not resolve host: HEAD
HTTP/1.1 200 OK
flag: picoCTF{r3j3ct_th3_du4l1ty_8f878508}
Content-type: text/html; charset=UTF-8

                                                                                                                                                 
┌──(kali㉿kali)-[~]
└─$
```

### Flag: picoCTF{r3j3ct_th3_du4l1ty_8f878508}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| curl | Curl es una herramienta de línea de comandos de Linux que sirve para transferir datos hacia o desde un servidor con URL, utilizando cualquiera de los protocolos soportados (HTTP, FTP, POP3, IMAP, SMTP, SCP, SFTP, TFTP, TELNET, LDAP…). |

## Referencias:
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods
- https://learn.onemonth.com/web-hacking-tools-proxies/