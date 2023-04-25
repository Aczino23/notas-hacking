# Includes

## Descripción: 
Can you get the flag?Go to this [website](http://saturn.picoctf.net:63115/) and see what you can discover.

**Pistas:**
1. Is there more code than what the inspector initially shows?

## Solución:
1. Inspeccionar el código fuente de la pagina: 

```css
body {
  background-color: lightblue;
}

/*  picoCTF{1nclu51v17y_1of2_  */
```

```js
function greetings()
{
  alert("This code is in a separate file!");
}

//  f7w_2of2_6edef411}
```

### Flag:  picoCTF{1nclu51v17y_1of2_f7w_2of2_6edef411}

## Notas adicionales:

## Referencias: