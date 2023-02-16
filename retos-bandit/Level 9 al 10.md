## Objetivo:
The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit9
- **Password:** EN632PlfYiZbn3PhVK3XOGSlNInNE00t

## Solución:
Revisamos que el archivo existe:

```bash
bandit9@bandit:~$ ls
data.txt
bandit9@bandit:~$
```

Intentamos buscarlo usando **``grep``**, pero al no ser un archivo de texto ASCII, no puede ser leído por este:

```bash
bandit9@bandit:~$ grep '=' data.txt
grep: data.txt: binary file matches
bandit9@bandit:~$
```

Por lo tanto, usamos el comando `strings`, quien nos imprime las cadenas de caracteres `imprimibles` en un archivo. El output de este comando lo redireccionamos a un **``grep``**, para buscar por varios **``=``**:

```bash
bandit9@bandit:~$ strings data.txt | grep '===='
c========== the
h;========== password
========== isT
n.E========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
bandit9@bandit:~$
```

## Notas adicionales:
El comando **``Strings``** básicamente imprime las cadenas de caracteres imprimibles en los archivos. A continuación se muestra su sintaxis:

```bash
strings [OPTIONS] FILENAME
```

El uso básico es bastante sencillo: basta con pasar el nombre del archivo como entrada y ejecutar el comando.

_Ten en cuenta que, como Strings se utiliza principalmente para extraer información de archivos binarios/ejecutables_

## Referencias:
- https://howtoforge.es/tutorial-de-comandos-de-cadenas-de-linux-para-principiantes-5-ejemplos/
