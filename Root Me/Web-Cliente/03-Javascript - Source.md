# Javascript - Source

## Descripción: 
¿Conoces el javascript?

[Empezar el reto](http://challenge01.root-me.org/web-client/ch1/)

## Solución:
Es bastante fácil, con solo ver el código fuente en cualquier navegador es posible realizarlo, en la comparación de la contraseña VS lo que el usuario escribe fácil de visualizar.

```html
<html>
    <head>
	<script type="text/javascript">
	/* <![CDATA[ */
	    function login(){
		pass=prompt("Entrez le mot de passe / Enter password");
		if ( pass == "123456azerty" ) {
		    alert("Mot de passe accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou can validate the challenge using this password.");  }
		else {
		    alert("Mauvais mot de passe / wrong password !");
		}
	    }
	/* ]]> */
	</script>
    </head>
   <body onload="login();"><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>

    </body>
</html>

```

### Flag: 123456azerty

## Notas adicionales:

## Referencias: