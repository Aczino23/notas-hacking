# Nombre del Reto

## Descripción: 

¿Conoces webpack?
Encontrar la contraseña.

[Empezar el reto](http://challenge01.root-me.org/web-client/ch27/)

## Solución:
Lo que hice fue:  
1. Ver el código fuente. (NADA) .
2. Ver todos los .js, tratar de desofuscarlo (NADA).  
3. Vi también que había algunos archivos .map y empecé a mirarlos:  
4. Con grep encontré una coincidencia con la palabra flag en app.a92c5074dafac0cb6365.js.map:

```bash
┌──(kali㉿kali)-[~]
└─$ curl -s  http://challenge01.root-me.org/web client/ch27/static/js/app.a92c5074dafac0cb6365.js.map | grep "flag"
```

5. Y así encontré la contraseña.

### Flag: BecauseSourceMapsAreGreatForDebuggingButNotForProduction

## Notas adicionales:

## Referencias:
- [Webpackjs - Devtool](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Webpackjs%20-%20Devtool.pdf) (Exploitation - Web)