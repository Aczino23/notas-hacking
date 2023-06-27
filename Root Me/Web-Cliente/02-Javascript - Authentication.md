# Javascript - Authentication

## Descripción: 
[Start the challenge](http://challenge01.root-me.org/web-client/ch9/)

## Solución:
1. Si se revisa el código fuente del html, encontrando el login.js, donde usando lógica de código vemos que el usuario y la contraseña están directamente escritos en el código.

```javascript
/* <![CDATA[ */

function Login(){
	var pseudo=document.login.pseudo.value;
	var username=pseudo.toLowerCase();
	var password=document.login.password.value;
	password=password.toLowerCase();
	if (pseudo=="4dm1n" && password=="sh.org") {
	    alert("Password accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou an validate the challenge using this password.");
	} else { 
	    alert("Mauvais mot de passe / wrong password"); 
	}
}
/* ]]> */ 
```

### Flag: sh.org

## Notas adicionales:

## Referencias:
