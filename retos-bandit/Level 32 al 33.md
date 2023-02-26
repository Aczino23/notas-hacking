## Objetivo:
After all this `git` stuff its time for another escape. Good luck!

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit32
- **Password:** rmCBvG56y58BXzv98yZGdO7ATVL5dW8y

## Solución:
En este reto, todo lo que escribimos en la `shell` es transformada a mayúsculas:

```bash
WELCOME TO THE UPPERCASE SHELL
>> ls
sh: 1: LS: not found
>> pwd
sh: 1: PWD: not found
>>
```

Por lo tanto, utilizamos `$0` para hacer referencia a la `shell` o al `script`, y esto nos trae una `shell sh` esto debido algo llamado  parámetros posicionales de un shell script.

```bash
>> $0
$ ls
uppershell
$ pwd
/home/bandit32
```

Revisamos que somos el usuario `bandit33` y obtenemos la password:

```bash
$ whoami
bandit33
$ cat /etc/bandit_pass/bandit33
odHo63fHiFqcWWJG9rLiLDtPm45KzUKy
$
```

## Notas adicionales:

### Parámetros posicionales

Es un tipo de variable de shell, almacenan los parámetros de entrada de un script. Tienen los nombres 0, 1, 2, ...y sus valores son $0, $1, $2...

Los parámetros posicionales son nombrados numéricamente a partir de 1 hasta N, donde N es el último argumento enviado al script. También existe el parámetro posicional 0, cuyo valor es el nombre del script invocado( o en defecto, la manera en que se invocó).

$* contiene a los parámetros posicionales, comenzando por el uno. Cuando la variable $* se encuentra entre comillas dobles, todos los parámetros son tratados como una sola unidad, esto ya que cada uno de los valores de los parámetros es separado por el primer carácter de la variable especial IFS. Si la variable IFS no está establecida, los parámetros se separan con espacios. Si IFS es nulo, los parámetros se unen sin utilizar ningún tipo de separador.

$@ contiene a los parámetros posicionales, empezando por el uno. Cuando la variable $@ se encuentra entre comillas dobles cada parámetro es tratado como una unidad separada del resto.

## Referencias:
- https://hablemoslinux.wordpress.com/2012/07/02/los-parametros-posicionales-en-un-shell-script/