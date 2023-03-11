## Objetivo:
Can you break into this super secure portal? `https://jupiter.challenges.picoctf.org/problem/29835/` ([link](https://jupiter.challenges.picoctf.org/problem/29835/)) or http://jupiter.challenges.picoctf.org:29835

**Hints:**
1. Never trust the client

## Solución:
1. Si inspeccionamos el código fuente de la página  podemos ver que existe una función en JavaScript que hace la validación de la contraseña:

```javascript
 function verify() {
    checkpass = document.getElementById("pass").value;
    split = 4;
    if (checkpass.substring(0, split) == 'pico') {
      if (checkpass.substring(split*6, split*7) == '723c') {
        if (checkpass.substring(split, split*2) == 'CTF{') {
         if (checkpass.substring(split*4, split*5) == 'ts_p') {
          if (checkpass.substring(split*3, split*4) == 'lien') {
            if (checkpass.substring(split*5, split*6) == 'lz_7') {
              if (checkpass.substring(split*2, split*3) == 'no_c') {
                if (checkpass.substring(split*7, split*8) == 'e}') {
                  alert("Password Verified")
                  }
                }
              }
      
            }
          }
        }
      }
    }
    else {
      alert("Incorrect password");
    }
  }
```

2. Al parecer esta función nos ayudara a obtener la bandera ya que la función realiza una validación muy simple de la contraseña que recibe por parte del usuario, dicha función realiza comparaciones de las subcadenas de la contraseña por lo tanto para obtener la bandera solo será necesario seguir el flujo de la función y ir ordenando las subcadenas para formar la bandera:  

```txt
split = 4;
if (checkpass.substring(0, split) == 'pico') {
      if (checkpass.substring(split*6, split*7) == '723c') {
        if (checkpass.substring(split, split*2) == 'CTF{') {
         if (checkpass.substring(split*4, split*5) == 'ts_p') {
          if (checkpass.substring(split*3, split*4) == 'lien') {
            if (checkpass.substring(split*5, split*6) == 'lz_7') {
              if (checkpass.substring(split*2, split*3) == 'no_c') {
                if (checkpass.substring(split*7, split*8) == 'e}') {
                  alert("Password Verified")

0,4 --> pico
4,8 --> CTF{
8,12 --> no_c
12,16 --> lien
16,20 --> ts_p
20,24 --> lz_7
24,28 --> 723c
28,32 --> e}

flag: picoCTF{no_clients_plz_7723ce}
```

### Flag: picoCTF{no_clients_plz_7723ce}

## Notas adicionales:

### Función substring de JavaScript: 

El método substring() es una función incorporada en JavaScript que se usa para extraer una parte de la cadena. Se pasan dos parámetros a la función, es decir, el índice inicial y el índice final que le dice a la función qué parte de la cadena tomar. Si el argumento pasado es negativo o NaN, se tratan como 0, y si los argumentos son mayores que la longitud de la cadena, se tratan igual que cadena.longitud

## Referencias:
- [client-side vs server-side](https://www.educative.io/answers/client-side-vs-server-side)
- [mozilla debugger](https://firefox-source-docs.mozilla.org/devtools-user/debugger/index.html)