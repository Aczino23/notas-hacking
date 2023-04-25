# Search source

## Descripción: 
The developer of this website mistakenly left an important artifact in the website source, can you find it?The website is [here](http://saturn.picoctf.net:53295/)

**Pistas:**
1. How could you mirror the website on your local machine so you could use more powerful tools for searching?

## Solución:
1. Al inspeccionar los archivos del código fuente de la pagina vemos que la flag se encuentra en un comentario en el archivo `style.ccs`: 

```css
}
...
 .navbar-expand-md .navbar-nav .nav-link {
     padding: 15px 48px;
     font-size: 16px;
     color: #000;
     line-height: 18px;
}
/** banner_main picoCTF{1nsp3ti0n_0f_w3bpag3s_8de925a7} **/
 .carousel-indicators li {
     width: 20px;
     height: 20px;
     border-radius: 11px;
     background-color: #070000;
}
 .carousel-indicators li.active {
    background-color: #35a30a;
...
```

### Flag: picoCTF{1nsp3ti0n_0f_w3bpag3s_8de925a7}

## Notas adicionales:

## Referencias: