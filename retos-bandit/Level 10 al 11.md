## Objetivo:
The password for the next level is stored in the file **data.txt**, which contains base64 encoded data.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit10
- **Password:** G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

## Solución:
Revisamos si el archivo **``data.txt``** se encuentra en nuestro directorio home, y leemos el archivo usando **``cat``**:

```bash
bandit10@bandit:~$ ls
data.txt
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIDZ6UGV6aUxkUjJSS05kTllGTmI2blZDS3pwaGxYSEJNCg==
bandit10@bandit:~$
```

Como se indicó en las instrucciones, el contenido del archivo es un string en [base64](https://en.wikipedia.org/wiki/Base64). Para estos casos, Linux posee una herramienta para codificar y decodificar la base mencionada.

Si revisamos el manual del comando **``base64``**, vemos que tiene una opción **``-d``**, que permite decodificar datos:

```bash
bandit10@bandit:~$ base64 --help
Usage: base64 [OPTION]... [FILE]
Base64 encode or decode FILE, or standard input, to standard output.

With no FILE, or when FILE is -, read standard input.

Mandatory arguments to long options are mandatory for short options too.
  -d, --decode          decode data
```

Por lo tanto, leemos el archivo con el comando y la opción para obtener la password del siguiente reto:

```bash
bandit10@bandit:~$ base64 -d data.txt
The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
bandit10@bandit:~$
```

## Notas adicionales:
El comando **``base64``** permite **codificar y descodificar cadenas de caracteres desde línea de comandos GNU/Linux**, en este caso desde BASH.

## Referencias:
- https://rm-rf.es/codificar-y-descodificar-base64-desde-bash/