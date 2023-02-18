## Objetivo:
The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL encryption.

**Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…**

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit15
- **Password:** jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

## Solución:
`openssl` viene con una herramienta de cliente que puede usar para conectarse a un servidor mediante una conexión segura. La herramienta es similar a `telnet` o `nc`, pero este utiliza SSL/TLS para la conexión.

El comando `s_client` implementa un cliente genérico SSL/TLS que se conecta a un host remoto mediante estos protocolos.

La opción `-connect` de `s_client` permite especificar el host y el puerto al cual nos vamos a conectar. El formato de este es `host:port`.  Cuando  nos conectamos, enviamos la password del usuario actual para obtener la password del siguiente reto:

```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = localhost
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = localhost
verify error:num=10:certificate has expired
notAfter=Feb 17 14:37:27 2023 GMT
verify return:1
depth=0 CN = localhost
notAfter=Feb 17 14:37:27 2023 GMT
verify return:1
---
Certificate chain
 0 s:CN = localhost
   i:CN = localhost
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA1
   v:NotBefore: Feb 17 14:36:27 2023 GMT; NotAfter: Feb 17 14:37:27 2023 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIDCzCCAfOgAwIBAgIEUU46AzANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjMwMjE3MTQzNjI3WhcNMjMwMjE3MTQzNzI3WjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC0
opHHs0Pjk84du/fcCwSAU9eeaTER3HOKN417mJEP3r/nDJoKYQ5hVLQBcgnz2KEg
dwAoDi9IFTW2XBbZcobd/xb+TcvdDvDVpc8oVX79EMMZMdXVqaiKA6TOA0p0nG4F
UWQZeB1eTGOVI5rsMDKMTtFzYEECUIxyWP5MLRquAJpBnsSIxCLfQ7sbEQNpLMXf
6eec2TmqLfLMvDWppo4NK6WCGA1hCg/21Ut1P+voaMto9XBUPr8d0mzfckldUyzG
ZtTI1F1AjT9IGIbgbS+P8XP8rZVTr/mVcufRTAKdLjh5WX8LdsKJ6CXrledPw21w
1WvCR6vaV1vP99Av2HwlAgMBAAGjZTBjMBQGA1UdEQQNMAuCCWxvY2FsaG9zdDBL
BglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0ZWQgYnkgTmNhdC4g
U2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3DQEBBQUAA4IBAQBe
2sqyCGHcpwNgCH5kk9anzixpyD45KKwxE7RM11Kt/v9YEYAFcpUI5QGIV1leArXS
7lqZgzh0lC6jmAOoKdjLrz2F9UBbU57VLP6veaBK3sf/ptE8vw4dSUYeNwhR6URg
M/4q6QYGmwIFcQjEZgt7CvLn6a7JgIvdo6ui9IuGUvCZ/X4JmfUyNQWdBuLQgVfv
mr4ZJX+R4Ri3pFfVmcG/B4B5yaiW17iRzqwvvewQ6ve6Hl6w0hdc1NLlbfc1BqMD
BkssdpTLp/Rl2nd90VMV5WhGEmOAAEPdVXq6eHK3cZhUaWhIJ6Bp7a+cy2YzaWNy
dkw4+kqaEE2YnPDTMRVc
-----END CERTIFICATE-----
```

```bash
read R BLOCK
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
Correct!
JQttfApK4SeyHwDlI9SXGR50qclOAil1

closed
bandit15@bandit:~$
```

## Notas adicionales:

| Comando | Descripción |
| --- | --- |
| openssl | OpenSSL es una biblioteca de software de criptografía o un juego de herramientas que hace que la comunicación a través de redes de computadoras sea más segura. El programa OpenSSL es una herramienta de línea de comandos para usar las diversas funciones de criptografía de la biblioteca de criptografía de OpenSSL desde el shell. |


## Referencias:
-   [Secure Socket Layer/Transport Layer Security on Wikipedia](https://en.wikipedia.org/wiki/Secure_Socket_Layer)
-   [OpenSSL Cookbook - Testing with OpenSSL](https://www.feistyduck.com/library/openssl-cookbook/online/ch-testing-with-openssl.html)