# Local Authority

## Descripción: 
Can you get the flag?Go to this [website](http://saturn.picoctf.net:64710/) and see what you can discover.

**Pistas:**
1. How is the password checked on this website?

## Solución:
1. Al pacer la validación del usurario y de la contraseña se realiza del lado del cliente con una función de JavaScript:  

```javascript
function checkPassword(username, password)
{
  if( username === 'admin' && password === 'strongPassword098765' )
  {
    return true;
  }
  else
  {
    return false;
  }
}
```

### Flag: picoCTF{j5_15_7r4n5p4r3n7_b0c2c9cb}

## Notas adicionales:

## Referencias: