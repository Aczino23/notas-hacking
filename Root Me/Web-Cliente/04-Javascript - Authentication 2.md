# Javascript - Authentication 2

## Descripción: 
Sí, amigos, Javascript es muy fácil :)

[Empezar el reto](http://challenge01.root-me.org/web-client/ch11/)

## Solución:
1. Al inspeccionar el código fuente de la pagina vemos que tenemos un archivo de JavaScript. Al analizar la lógica del código podemos observar que el usuario y la contraseña se encentran en la variable `TheLists`, en donde el usuario es `GOD` y la contraseña `HIDDEN`. 

```javascript
function connexion(){
    var username = prompt("Username :", "");
    var password = prompt("Password :", "");
    var TheLists = ["GOD:HIDDEN"];
    for (i = 0; i < TheLists.length; i++)
    {
        if (TheLists[i].indexOf(username) == 0)
        {
            var TheSplit = TheLists[i].split(":");
            var TheUsername = TheSplit[0];
            var ThePassword = TheSplit[1];
            if (username == TheUsername && password == ThePassword)
            {
                alert("Vous pouvez utiliser ce mot de passe pour valider ce challenge (en majuscules) / You can use this password to validate this challenge (uppercase)");
            }
        }
        else
        {
            alert("Nope, you're a naughty hacker.")
        }
    }
}
```

### Flag: HIDDEN

## Notas adicionales:

## Referencias: