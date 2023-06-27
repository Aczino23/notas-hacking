# Lab: Reflected XSS into HTML context with nothing encoded

## Descripción: 
This lab contains a simple [reflected cross-site scripting](https://portswigger.net/web-security/cross-site-scripting/reflected) vulnerability in the search functionality.

To solve the lab, perform a cross-site scripting attack that calls the `alert` function. 

## Solución:
1. Copie y pegue lo siguiente en el cuadro de búsqueda:

```javascript
<script>alert(1)</script>
```

![Pasted image 20230627133553](Pasted%20image%2020230627133553.png)

2. Haga clic en "Buscar".

![Pasted image 20230627133653](Pasted%20image%2020230627133653.png)

etryt
## Notas adicionales:


## Referencias: