# Javascript - Obfuscation 3

## Descripción: 
Útil o Inútil esa es la cuestión...
[Empezar el reto](http://challenge01.root-me.org/web-client/ch13/ch13.html)

## Solución:
1. Lo primero que hacemos es inspeccionar el código fuente de la pagina: 

```html
<html>
<head>
    <title>Obfuscation JS</title>
    <script type="text/javascript">
    function dechiffre(pass_enc){
        var pass = "70,65,85,88,32,80,65,83,83,87,79,82,68,32,72,65,72,65";
        var tab  = pass_enc.split(',');
                var tab2 = pass.split(',');var i,j,k,l=0,m,n,o,p = "";i = 0;j = tab.length;
                        k = j + (l) + (n=0);
                        n = tab2.length;
                        for(i = (o=0); i < (k = j = n); i++ ){o = tab[i-l];p += String.fromCharCode((o = tab2[i]));
                                if(i == 5)break;}
                        for(i = (o=0); i < (k = j = n); i++ ){
                        o = tab[i-l]; 
                                if(i > 5 && i < k-1)
                                        p += String.fromCharCode((o = tab2[i]));
                        }
        p += String.fromCharCode(tab2[17]);
        pass = p;return pass;
    }
    String["fromCharCode"](dechiffre("\x35\x35\x2c\x35\x36\x2c\x35\x34\x2c\x37\x39\x2c\x31\x31\x35\x2c\x36\x39\x2c\x31\x31\x34\x2c\x31\x31\x36\x2c\x31\x30\x37\x2c\x34\x39\x2c\x35\x30"));
    
    h = window.prompt('Entrez le mot de passe / Enter password');
    alert( dechiffre(h) );
    
</script>
</head>

</html>
```

2. Al analizar el código de la pagina nos damos cuenta que existe una función de JavaScript llamada `dechiffre` la cual al parecer es la que se encarga de descifrar la contraseña por lo tanto lo primero que hacemos es hacer lo siguiente:  

```JavaScript
console.log("\x35\x35\x2c\x35\x36\x2c\x35\x34\x2c\x37\x39\x2c\x31\x31\x35\x2c\x36\x39\x2c\x31\x31\x34\x2c\x31\x31\x36\x2c\x31\x30\x37\x2c\x34\x39\x2c\x35\x30");
```

3. Al imprimir lo anterior obtenemos `55,56,54,79,115,69,114,116,107,49,50`, después con ayuda de la herramienta [CyberChef](https://gchq.github.io/CyberChef/) obtenemos la contraseña: ``

### Flag: 786OsErtk12

## Notas adicionales:

## Referencias:
- [Automatic simplification of obfuscated JavaScript code](https://repository.root-me.org/Virologie/EN%20-%20Automatic%20simplification%20of%20obfuscated%20JavaScript%20code.pdf) 
- [Spiffy: Automated JavaScript deobfuscation](https://repository.root-me.org/Virologie/EN%20-%20Spiffy:%20Automated%20JavaScript%20deobfuscation.pdf) 
- [Automatic detection for javaScript obfuscation attacks](https://repository.root-me.org/Virologie/EN%20-%20Automatic%20detection%20for%20javaScript%20obfuscation%20attacks.pdf) 
- [DEFCON a different approach to JavaScript obfuscation](https://repository.root-me.org/Virologie/EN%20-%20DEFCON%20a%20different%20approach%20to%20JavaScript%20obfuscation.pdf) 