## Objetivo:
This website can be rendered only by **picobrowser**, go and catch the flag! `https://jupiter.challenges.picoctf.org/problem/50522/` ([link](https://jupiter.challenges.picoctf.org/problem/50522/)) or http://jupiter.challenges.picoctf.org:50522

**Hints:**
1. You don't need to download a new web browser

## Solución:

```bash
┌──(kali㉿kali)-[~]
└─$ curl --help                                                                                   
Usage: curl [options...] <url>
 -d, --data <data>          HTTP POST data
 -f, --fail                 Fail fast with no output on HTTP errors
 -h, --help <category>      Get help for commands
 -i, --include              Include protocol response headers in the output
 -o, --output <file>        Write to file instead of stdout
 -O, --remote-name          Write output to a file named as the remote file
 -s, --silent               Silent mode
 -T, --upload-file <file>   Transfer local FILE to destination
 -u, --user <user:password> Server user and password
 -A, --user-agent <name>    Send User-Agent <name> to server
 -v, --verbose              Make the operation more talkative
 -V, --version              Show version number and quit

This is not the full help, this menu is stripped into categories.
Use "--help category" to get an overview of all categories.
For all options use the manual or "--help all".

┌──(kali㉿kali)-[~]
└─$ curl -s https://jupiter.challenges.picoctf.org/problem/50522/flag -A "picobrowser" | grep picoCTF
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{p1c0_s3cr3t_ag3nt_51414fa7}</code></p>
                                                                                                                                                                             
┌──(kali㉿kali)-[~]
└─$
```

### Flag: picoCTF{p1c0_s3cr3t_ag3nt_51414fa7}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| curl | Curl es una herramienta de línea de comandos de Linux que sirve para transferir datos hacia o desde un servidor con URL, utilizando cualquiera de los protocolos soportados (HTTP, FTP, POP3, IMAP, SMTP, SCP, SFTP, TFTP, TELNET, LDAP…). |

### Qué es User-Agent:
El user-agent es un campo del protocolo HTTP que puede utilizarse para transmitir información más o menos detallada sobre el dispositivo de consulta que efectúa una petición de red.

Esto se hace a través de la cabecera HTTP y esta información puede utilizarse, por ejemplo, para entregar ciertos elementos sólo a aquellos navegadores que se sabe que son capaces de manejarlos.

La sintaxis del user-agent es muy sencilla:

```txt
User-Agent: <Producto> / <Versión del producto> <Comentarios>
```

## Referencias:
- https://developer.mozilla.org/es/docs/Web/HTTP/Headers/User-Agent