# Javascript - Obfuscation 1

## Descripción: 
[Empezar el reto](http://challenge01.root-me.org/web-client/ch4/ch4.html)

## Solución:
1. Al inspeccionar el código fuente de la pagina encontramos lo siguiente:

```html
<html>
    <head>
        <title>Obfuscation JS</title>

          <script type="text/javascript">
              /* <![CDATA[ */

              pass = '%63%70%61%73%62%69%65%6e%64%75%72%70%61%73%73%77%6f%72%64';
              h = window.prompt('Entrez le mot de passe / Enter password');
              if(h == unescape(pass)) {
                  alert('Password accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou an validate the challenge using this pass.');
              } else {
                  alert('Mauvais mot de passe / wrong password');
              }

              /* ]]> */
          </script>
    </head>
   <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    </body>
</html>

```


2. Al analizar el código nos damos cuenta que la contraseña esta ofuscada. Así haciendo uso de la función  `unescape` logramos obtener la contraseña: 

```javascript
pass = '%63%70%61%73%62%69%65%6e%64%75%72%70%61%73%73%77%6f%72%64';

console.log(unescape(pass))

// Contraseña
//'cpasbiendurpassword'
```

### Flag: cpasbiendurpassword

## Notas adicionales:

**`unescape()`** es una propiedad de función del objeto global.

La función `unescape()` reemplaza cualquier secuencia de escape con el carácter que representa. Específicamente, reemplaza cualquier secuencia de escape de la forma `%XX` o `%uXXXX` (donde `X`representa un dígito hexadecimal) con el carácter que tiene el valor hexadecimal `XX`/`XXXX`. Si la secuencia de escape no es una secuencia de escape válida (por ejemplo, si "%" va seguido de uno o ningún dígito hexadecimal), se deja como está.

## Referencias:
- [Automatic simplification of obfuscated JavaScript code](https://repository.root-me.org/Virologie/EN%20-%20Automatic%20simplification%20of%20obfuscated%20JavaScript%20code.pdf) 
- [Spiffy: Automated JavaScript deobfuscation](https://repository.root-me.org/Virologie/EN%20-%20Spiffy:%20Automated%20JavaScript%20deobfuscation.pdf) 
- [Automatic detection for javaScript obfuscation attacks](https://repository.root-me.org/Virologie/EN%20-%20Automatic%20detection%20for%20javaScript%20obfuscation%20attacks.pdf) 
- [DEFCON a different approach to JavaScript obfuscation](https://repository.root-me.org/Virologie/EN%20-%20DEFCON%20a%20different%20approach%20to%20JavaScript%20obfuscation.pdf) 