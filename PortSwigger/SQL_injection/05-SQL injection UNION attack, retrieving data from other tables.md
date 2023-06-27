# Lab: SQL injection UNION attack, retrieving data from other tables

## Descripción: 
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs.

The database contains a different table called `users`, with columns called `username` and `password`.

To solve the lab, perform a [SQL injection UNION](https://portswigger.net/web-security/sql-injection/union-attacks) attack that retrieves all usernames and passwords, and use the information to log in as the `administrator` user.

## Solución:
1. Usamos Burp Suite para interceptar y modificar la solicitud que establece el filtro de categoría de producto.

![Pasted image 20230626172143](Pasted%20image%2020230626172143.png)

2. Determine el [número de columnas que devuelve la consulta](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns) y [cuál las columnas contienen datos de texto](https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text). Verifique que la consulta devuelva dos columnas, las cuales contienen texto, usando un payload como la siguiente en el parámetro de categoría:  `'+UNION+SELECT+'abc','def'--`

![Pasted image 20230627131827](Pasted%20image%2020230627131827.png)

![Pasted image 20230627131908](Pasted%20image%2020230627131908.png)

![Pasted image 20230627132202](Pasted%20image%2020230627132202.png)

3. Usamos el siguiente payload para recuperar el contenido de la tabla `users` :`'+UNION+SELECT+username,+password+FROM+users--`

![Pasted image 20230627132413](Pasted%20image%2020230627132413.png)

4. Verifique que la respuesta de la aplicación contenga nombres de usuario y contraseñas.

![Pasted image 20230627132557](Pasted%20image%2020230627132557.png)


![Pasted image 20230627132634](Pasted%20image%2020230627132634.png)

5. Vemos que obtenemos el usuario y la contraseña del administrador nos logueamos en en el sitio y resolvemos el laboratorio. 

## Notas adicionales:

### Unión:
El operador de Unión combina los resultados de dos o más consultas dando lugar a la creación de un único conjunto de resultados que incluye todas las filas que pertenecen a todas las consultas en la Unión. En esta operación, combina dos consultas más y elimina los duplicados.

## Referencias:
- https://portswigger.net/web-security/sql-injection/union-attacks
- https://www.sqlshack.com/es/revision-ejemplos-y-uso-de-sql-union/#:~:text=El%20operador%20UNION%20combina%20los,filas%20y%20mantiene%20los%20duplicados.