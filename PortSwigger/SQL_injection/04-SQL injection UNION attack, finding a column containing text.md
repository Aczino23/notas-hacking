# Lab: SQL injection UNION attack, finding a column containing text

## Descripción: 
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you first need to determine the number of columns returned by the query. You can do this using a technique you learned in a [previous lab](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns). The next step is to identify a column that is compatible with string data.

The lab will provide a random value that you need to make appear within the query results. To solve the lab, perform a [SQL injection UNION](https://portswigger.net/web-security/sql-injection/union-attacks) attack that returns an additional row containing the value provided. This technique helps you determine which columns are compatible with string data.

## Solución:
1. Usamos Burp Suite para interceptar y modificar la solicitud que establece el filtro de categoría de producto.

![Pasted image 20230626165018](Pasted%20image%2020230626165018.png)

2. Determinamos el número de columnas que devuelve la consulta. Verifique que la consulta devuelva tres columnas, utilizando la siguiente carga útil en el parámetro de categoría: `'+UNION+SELECT+NULL,NULL,NULL--`

![Pasted image 20230626165438](Pasted%20image%2020230626165438.png)

![Pasted image 20230626165615](Pasted%20image%2020230626165615.png)

3. Intentamos reemplazar cada nulo con el valor aleatorio proporcionado por el laboratorio, por ejemplo: `'+UNION+SELECT+NULL,'3uI67r',NULL--` 

- Hacemos que la base de datos recupere la cadena: `'3uI67r'`

![Pasted image 20230626171049](Pasted%20image%2020230626171049.png)

![Pasted image 20230626171125](Pasted%20image%2020230626171125.png)

## Notas adicionales:

### Unión:
El operador de Unión combina los resultados de dos o más consultas dando lugar a la creación de un único conjunto de resultados que incluye todas las filas que pertenecen a todas las consultas en la Unión. En esta operación, combina dos consultas más y elimina los duplicados.

## Referencias:
- https://portswigger.net/web-security/sql-injection/union-attacks
- https://www.sqlshack.com/es/revision-ejemplos-y-uso-de-sql-union/#:~:text=El%20operador%20UNION%20combina%20los,filas%20y%20mantiene%20los%20duplicados.