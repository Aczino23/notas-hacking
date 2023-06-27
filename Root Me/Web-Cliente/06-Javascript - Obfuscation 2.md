# Javascript - Obfuscation 2

## Descripción: 

Bajando 3 pisos.....
[Empezar el reto](http://challenge01.root-me.org/web-client/ch12/ch12.html)

## Solución:
1. Al inspeccionar el código fuente de la pagina encontramos lo siguiente: 

```html
<html>

<head>
	<title>Obfuscation JS</title>
<!-- 
Obfuscation 
.Niveau : Facile 
.By Hel0ck
.The mission : 
	Retrouver le password contenu dans la var pass.
	You need my help ? IRC : irc.root-me.org #root-me
-->
<script type="text/javascript">
	var pass = unescape("unescape%28%22String.fromCharCode%2528104%252C68%252C117%252C102%252C106%252C100%252C107%252C105%252C49%252C53%252C54%2529%22%29");
</script>
</head>

</html>
```

2. Al analizar el código anterior observamos que tenemos una variable llamada `pass` que al parecer esta ofuscada, por lo tano al desofuscar el código obtenemos siguiente:

```Javascript
var pass = unescape("unescape%28%22String.fromCharCode%2528104%252C68%252C117%252C102%252C106%252C100%252C107%252C105%252C49%252C53%252C54%2529%22%29");
undefined

pass
'unescape("String.fromCharCode%28104%2C68%2C117%2C102%2C106%2C100%2C107%2C105%2C49%2C53%2C54%29")'

unescape('%28104%2C68%2C117%2C102%2C106%2C100%2C107%2C105%2C49%2C53%2C54%29')
'(104,68,117,102,106,100,107,105,49,53,54)'
```

3. Obtenemos la siguiente cadena: '`(104,68,117,102,106,100,107,105,49,53,54)'` con ayuda de la herramienta [CyberChef](https://gchq.github.io/CyberChef/) descodificamos la cadena y obtenemos la contraseña.

### Flag: hDufjdki156

## Notas adicionales:


## Referencias: