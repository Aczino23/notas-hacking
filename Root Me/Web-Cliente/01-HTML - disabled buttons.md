# HTML - disabled buttons

## Descripción: 
Este formulario está desactivado y no puede ser utilizado. Depende de ti encontrar la manera de usarlo.

[Empezar el reto](http://challenge01.root-me.org/web-client/ch25/)

## Solución:
- Es un problema sencillo primero debemos ejecutar el inspector de nuestro navegador y buscamos los input deshabilitados  luego editamos el atributo disable eliminándolo y listo solo digitamos algo en el input text  como nuestro usuario y le damos click al botón y nos aparecerá la contraseña.

```html
<html>
    <head>
        <title>Under construction</title>
        <link rel='stylesheet' property='stylesheet' type='text/css' href='style.css' media='all' />
    </head>
   <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
        <h1>Website temporarily closed.</h1>
        <hr>

        <form action="" method="post" name="authform">
            <div>
                <input disabled type="text" name="auth-login" value="" />
                <input disabled type="submit" value="Member access" name="authbutton" />
            </div>
        </form>
            </body>
</html>
```

![Pasted image 20230615154215](Pasted%20image%2020230615154215.png)


### Flag: HTMLCantStopYou

## Notas adicionales:

El atributo **disabled** de HTML **es un atributo de tipo booleano**. Es decir, al igual que el atributo required de HTML, su función se ejecuta con tan solo estar presente dentro de la etiqueta; no necesita de ningún valor específico. Puntualmente, este atributo nos permite interactuar con la etiqueta button.

## Referencias:
- Sin referencias 