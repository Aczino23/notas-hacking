## Objetivo:
The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit8
- **Password:** TESKZC0XvTetK0S9xNwm25STk5iWrBvP

## Solución:
Validamos que el archivo existe:

```bash
bandit8@bandit:~$ ls
data.txt
bandit8@bandit:~$
```

Para buscar líneas únicas en un archivo usamos el comando **``uniq``** con la opción **``-u``**:

```bash
bandit8@bandit:~$ uniq -u data.txt
puP3nfQp5FCMNyLsdWASZ472scVSrUDJ
desthMrvBwFuSWkom7FP8ASJayNlfoRd
7XS0q7U1mnlcxKF8TqKmV0MTz3Nk2JLR
7Yw8BBU0dsNPIPGaqTrzCD1ui5ZUPC3W
bpGBMUddF6EGDkaXM8uguzsgQ9hVMX5x
WMPIYAeOF4iIKjo4ZC9ux57X5Tzukk5W
9g8tRRuUhXrOYgdQohBAvxas7CB939F4
i1F09GVEcOpA740WJJc1DELRUhfGCHl9
nzs4ijk2uOZItbx4Le3Zyugvp68xXkpp
p1dzDa5gJ8tpkgPW5hPHDRENabkbbYFV
HOqQ9Z3JVL1A05MoavjtZzng1CkauWGg
qwMRqzTYYCX2ztxsXTdlfdSBBlmMAmoK
qabqd0h14Dp7L4SNqpLwhhfgxdiMX5Xe
Sb6wvmTLpr10L22TD9oatJEvHleOaJOf
5c8VjsZCxYC9eRLNFnXq58TBsS0oYnhl
...
```

Se nos presenta el primer problema, que es el desorden del texto. Para encontrar la solución, ordenamos el contenido del archivo usando la herramienta **``sort``**:

```bash
bandit8@bandit:~$ sort data.txt
0nWWiILKIHjVQhAySQCVA1OO4pRFzm0g
0nWWiILKIHjVQhAySQCVA1OO4pRFzm0g
0nWWiILKIHjVQhAySQCVA1OO4pRFzm0g
0nWWiILKIHjVQhAySQCVA1OO4pRFzm0g
0nWWiILKIHjVQhAySQCVA1OO4pRFzm0g
0nWWiILKIHjVQhAySQCVA1OO4pRFzm0g
0nWWiILKIHjVQhAySQCVA1OO4pRFzm0g
0nWWiILKIHjVQhAySQCVA1OO4pRFzm0g
0nWWiILKIHjVQhAySQCVA1OO4pRFzm0g
...
```

Ahora que el texto se encuentra ordenado, podemos redireccionar la salida del comando `sort` al comando **``uniq -u``** a través del símbolo **``|``**:

```bash
bandit8@bandit:~$ sort data.txt | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
bandit8@bandit:~$
```

## Notas adicionales:
El comando **``sort``** se usa para ordenar las líneas en un archivo de texto. Su sintaxis es:

```bash
sort [opciones] nombre_de_archivo
```

El comando **_uniq_** suprime o informa de líneas duplicadas consecutivas que contiene un fichero o la entrada estándar.
La sintaxis general es:

```bash
uniq  [opción...]  [ fichero_entrada  [fichero_salida] ]
```

La opción _**-u**_ nos muestra solo las líneas no repetidas:

## Referencias:
- https://www.hscripts.com/es/tutoriales/linux-commands/sort.html
- https://www.fpgenred.es/GNU-Linux/uniq.html#:~:text=El%20comando%20uniq%20suprime%20o,fichero%20o%20la%20entrada%20est%C3%A1ndar.