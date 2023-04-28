# SQL Direct

## Descripción: 
Connect to this PostgreSQL server and find the flag!
Additional details will be available after launching your challenge instance.

Connect to this PostgreSQL server and find the flag!`psql -h saturn.picoctf.net -p 52118 -U postgres pico`Password is `postgres`

**Pistas:**
1. What does a SQL database contain?

## Solución:
1. Primero nos conectamos:

```bash
┌──(kali㉿kali)-[~]
└─$ psql -h saturn.picoctf.net -p 52118 -U postgres pico  
Contraseña para usuario postgres: 
psql (15.2 (Debian 15.2-2))
Digite «help» para obtener ayuda.

pico=# 
```

2. Ahora listemos con `\l+` todas las bases de datos:

```bash
pico=# \l+
                                                                                      Listado de base de datos
  Nombre   |  Dueño   | Codificación |  Collate   |   Ctype    | configuración ICU | Proveedor de locale |      Privilegios      | Tamaño  | Tablespace |                Descripción                 
-----------+----------+--------------+------------+------------+-------------------+---------------------+-----------------------+---------+------------+--------------------------------------------
 pico      | postgres | UTF8         | en_US.utf8 | en_US.utf8 |                   | libc                |                       | 7485 kB | pg_default | 
 postgres  | postgres | UTF8         | en_US.utf8 | en_US.utf8 |                   | libc                |                       | 7453 kB | pg_default | default administrative connection database
 template0 | postgres | UTF8         | en_US.utf8 | en_US.utf8 |                   | libc                | =c/postgres          +| 7297 kB | pg_default | unmodifiable empty database
           |          |              |            |            |                   |                     | postgres=CTc/postgres |         |            | 
 template1 | postgres | UTF8         | en_US.utf8 | en_US.utf8 |                   | libc                | =c/postgres          +| 7525 kB | pg_default | default template for new databases
           |          |              |            |            |                   |                     | postgres=CTc/postgres |         |            | 
(4 filas)

pico=# 
```

3. Ahora listemos con `\dt` . Encontramos la tabla de `flags` en su interior. Hacemos un listado de la tabla de `flags` con `select * from flags;` 

```bash
pico=# \dt
        Listado de relaciones
 Esquema | Nombre | Tipo  |  Dueño   
---------+--------+-------+----------
 public  | flags  | tabla | postgres
(1 fila)

pico=#
```

4. Encontramos la flag: 

```bash
pico=# select * from flags;
 id | firstname | lastname  |                address                 
----+-----------+-----------+----------------------------------------
  1 | Luke      | Skywalker | picoCTF{L3arN_S0m3_5qL_t0d4Y_31fd14c0}
  2 | Leia      | Organa    | Alderaan
  3 | Han       | Solo      | Corellia
(3 filas)

pico=# 
```

### Flag: picoCTF{L3arN_S0m3_5qL_t0d4Y_31fd14c0}

## Notas adicionales:

## PostgreSQL 
PostgreSQL es un servidor de base de datos objeto relacional libre, ya que incluye características de la orientación a objetos, como puede ser la herencia, tipos de datos, funciones, restricciones, disparadores, reglas e integridad transaccional, liberado bajo la licencia BSD. Como muchos otros proyectos open source, el desarrollo de PostgreSQL no es manejado por una sola compañía sino que es dirigido por una comunidad de desarrolladores y organizaciones comerciales las cuales trabajan en su desarrollo, dicha comunidad es denominada el PGDG (PostgreSQL Global Development Group).

## Referencias:
- https://apuntes-snicoper.readthedocs.io/es/latest/programacion/postgresql/comandos_consola_psql.html