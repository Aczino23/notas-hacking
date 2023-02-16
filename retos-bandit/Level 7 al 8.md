## Objetivo:
The password for the next level is stored in the file **data.txt** next to the word **millionth**

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit7
- **Password:** z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

## Solución:
Revisamos si el archivo existe en el directorio actual, y lo leemos:

```bash
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$
```

Al ejecutar **``cat``** al archivo, vemos que aparecen miles de líneas de texto, por lo tanto, se nos complica un poco la búsqueda. Para que sea más fácil, utilizamos la herramienta **``grep``**, que nos permite filtrar por texto.

```bash
mammal  N1TF6BzlzQLjZseO6jHbOaOLb7K47Fqc
enema's 82tHGaDkIvNI1Dmifno7vXOxTDA37ipb
schemer's       nDtSQFHG4jwrZshY1W9acUOQFYp00x0X
Cochise zcsApVgeaK4ReCaew9twT2EKzurX8TwJ
Wooten's        JeqzlOrZH9TGKv960z9WnecVu68uDeQK
counsel Edd9WXhk9qNyqSy5czR4aYC1gipmcXFV
dipsomania's    sW3Ah5QHInyiux9ImIcsCG57akrMZ6aG
conjoins        ya71ItSkbB9T7A2NenU7ZYailifsj29L
watchers        VTkcqne6AVaPCp7Nv6d2EjyxxjHQYp7v
salami  d7GZcuqLjIfcn0huMlLwhRp5rBY9y3rW
Rudolph's       GTGDVWy5JKi5QAxxdnLA6mfnxIw45x7D
.....
```

Como `grep` nos permite filtrar por texto, buscamos por la palabra que se encuentra antes de la password (**``millionth``**):

```bash
bandit7@bandit:~$ cat data.txt | grep millionth
millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP
bandit7@bandit:~$
```

## Notas adicionales:
El comando **``grep``**, si ya estas familiarizado con la consola, es un comando que nos sirve para buscar palabras, símbolos, letras, números y cualquier patrón dentro de un archivo. Es muy común ya que puede ser que en un archivo gigante, como por ejemplo en un archivo que contenga la traducción de una película importante nosotros hayamos usado la palabra man cuando era men. En ese caso, grep nos ayuda a encontrar cuantas veces usamos esa palabra y la línea en donde es usada. Además de que sirve para otras cosas. Entonces, podemos decir que es sumamente útil y de seguro tu le encontraras muchos usos.

## Referencias:

- https://platzi.com/blog/como-usar-el-comando-grep-en-la-consola-y-porque-es-importante-en-las-regexp/?utm_source=google&utm_medium=cpc&utm_campaign=19643931773&utm_adgroup=&utm_content=

- https://www.hostinger.mx/tutoriales/comando-grep-linux