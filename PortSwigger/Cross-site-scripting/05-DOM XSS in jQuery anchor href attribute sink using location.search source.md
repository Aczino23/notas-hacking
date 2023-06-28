# Lab: DOM XSS in jQuery anchor `href` attribute sink using `location.search` source

## Descripción: 
This lab contains a [DOM-based cross-site scripting](https://portswigger.net/web-security/cross-site-scripting/dom-based) vulnerability in the submit feedback page. It uses the jQuery library's `$` selector function to find an anchor element, and changes its `href` attribute using data from `location.search`.
To solve this lab, make the "back" link alert `document.cookie`.

## Solución:
1. En la página Submit feedback, cambie el parámetro de consulta `returnPath` a / seguido de una cadena alfanumérica aleatoria.

2. Haga clic derecho e inspeccione el elemento, y observe que su cadena aleatoria se ha colocado dentro de un atributo `href`.

![Pasted image 20230628142408](Pasted%20image%2020230628142408.png)

3. Cambiamos la ruta de retorno (`returnPath`) a:

```javascript
javascript:alert(document.cookie)
```

4. Haz clic en el botón de `Back`.

## Notas adicionales:

El payload `javascript:alert(document.cookie)` es una URL JavaScript que se puede ejecutar en un navegador web. Al abrir esta URL en el navegador, se ejecuta la función `alert()` con el contenido de la propiedad `document.cookie`.

La propiedad `document.cookie` contiene las cookies asociadas al sitio web actual. Las cookies son pequeños archivos de texto que se utilizan para almacenar información en el navegador del usuario, como preferencias, información de inicio de sesión o datos de seguimiento.

Al ejecutar `alert(document.cookie)`, se mostrará una ventana emergente (alerta) en el navegador con el contenido de las cookies para el sitio web en el que se está ejecutando el código. Esto significa que cualquier cookie almacenada para ese sitio web será mostrada en la alerta.

## Referencias:
- https://portswigger.net/web-security/cross-site-scripting/dom-based