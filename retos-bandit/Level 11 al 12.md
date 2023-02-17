## Objetivo:
The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit11
- **Password:** 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

## Solución:
Revisamos el archivo **``data.txt``**, y encontramos que los datos de este no tienen sentido:

```bash
bandit11@bandit:~$ ls
data.txt
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi
bandit11@bandit:~$
```

Siguiendo las instrucciones, vemos que las letras originales fueron reemplazadas por una letra 13 posiciones después del alfabeto.

Como ejemplo, pasaremos la palabra hello a ROT13:

-   Si a la letra `H` la movemos 13 lugares en el [alfabeto inglés](https://www.inglessencillo.com/el-alfabeto), quedaría con la letra `U`
-   Si hacemos lo mismo con la `E`, sería `R`
-   La `L` sería `Y`
-   Y la `O` sería `B`

Entonces, si pasamos la palabra **`hello`** a ROT13, quedaría **`uryyb`**.

Ahora que sabemos como usar ROT13, lo que haremos es usar el comando `tr`, que nos permite traducir o eliminar caracteres. Por lo tanto, usando este método, moveremos la letra **`A`** 13 posiciones, quedando en la letra **`N`**, y así con cada carácter.

Al usar `tr`, primero escribimos todos los caracteres a traducir (mayúsculas y minúsculas) **`'A-Za-z'`** Luego indicamos los caracteres movidos 13 posiciones **``'N-ZA-Nn-za-m'``**:

```bash
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
bandit11@bandit:~$
```

## Notas adicionales:

| Comando | Descripción |
| --- | ---| ---|
| tr | `tr` es una utilidad de línea de comandos en sistemas Linux y Unix que traduce, elimina y exprime caracteres de la entrada estándar y escribe el resultado en la salida estándar.

- El comando **`tr`** puede realizar operaciones como eliminar caracteres repetidos, convertir mayúsculas a minúsculas y reemplazar y eliminar caracteres básicos. Por lo general, se usa en combinación con otros comandos a través de tuberías.

| 23 | ldf |
| ---- | --- |



## Referencias:
- https://es.joecomp.com/tr-command-linux-with-examples