## Objetivo:
Can you find the robots? `https://jupiter.challenges.picoctf.org/problem/60915/` ([link](https://jupiter.challenges.picoctf.org/problem/60915/)) or http://jupiter.challenges.picoctf.org:60915

**Hints:**
1. What part of the website could tell you where the creator doesn't want you to look?

## Solución:
1. Primero modificamos la URL de la pagina para ver si tiene un archivo robots.txt:

```txt
http://jupiter.challenges.picoctf.org:60915/robots.txt
```

2. Vemos que la pagina si tiene un archivo robots en el cual encontramos los siguiente: 

```txt
User-agent: *
Disallow: /8028f.html
```

3. Vamos a la ruta http://jupiter.challenges.picoctf.org:60915/8028f.html para obtener la bandera:

```txt
Guess you found the robots  
picoCTF{ca1cu1at1ng_Mach1n3s_8028f}
```

### Flag: picoCTF{ca1cu1at1ng_Mach1n3s_8028f}

## Notas adicionales:

### Archivos Robots.txt:
Robots.txt son archivos utilizados para favorecer la navegación de un algoritmo de búsqueda en un sitio web, orientando cuáles páginas deben ser indexadas en los buscadores y controlando las páginas a las que el robot del motor de búsqueda no debe acceder.

## Referencias:
1. https://developers.google.com/search/docs/crawling-indexing/robots/intro?hl=es