# Lab: Reflected XSS into HTML context with nothing encoded

## Descripción: 
This lab contains a simple [reflected cross-site scripting](https://portswigger.net/web-security/cross-site-scripting/reflected) vulnerability in the search functionality.

To solve the lab, perform a cross-site scripting attack that calls the `alert` function. 

## Solución:
1. Copie y pegue lo siguiente en el cuadro de búsqueda:

```html
<script>alert(1)</script>
```

![Pasted image 20230627135214](Pasted%20image%2020230627135214.png)

2. Haga clic en "Buscar".

![Pasted image 20230627135723](Pasted%20image%2020230627135723.png)

## Notas adicionales:

### Cross-site scripting:
Cross-site scripting (también conocido como XSS) es una vulnerabilidad de seguridad web que permite a un atacante comprometer las interacciones que los usuarios tienen con una aplicación vulnerable. Permite a un atacante eludir la misma política de origen, que está diseñada para segregar diferentes sitios web entre sí. Las vulnerabilidades de secuencias de comandos entre sitios normalmente permiten que un atacante se haga pasar por un usuario víctima, lleve a cabo cualquier acción que el usuario pueda realizar y acceda a cualquiera de los datos del usuario. Si el usuario de la víctima tiene acceso privilegiado dentro de la aplicación, entonces el atacante podría obtener control total sobre toda la funcionalidad y los datos de la aplicación. 

## Referencias:
- https://portswigger.net/web-security/cross-site-scripting#what-is-cross-site-scripting-xss