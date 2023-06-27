# Lab: SQL injection UNION attack, determining the number of columns returned by the query

## Descripción: 
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack.

To solve the lab, determine the number of columns returned by the query by performing a [SQL injection UNION](https://portswigger.net/web-security/sql-injection/union-attacks) attack that returns an additional row containing null values.

## Solución:
1. Utilizamos Burp Suite para interceptar y modificar la solicitud que establece el filtro de categoría de producto.

![Pasted image 20230626162946](Pasted%20image%2020230626162946.png)

2. Modificamos el parámetro `category` , dándole el valor `'+UNION+SELECT+NULL--`.  y observamos que se produce un error.
 
![Pasted image 20230626163203](Pasted%20image%2020230626163203.png)

3. Modificamos el parámetro `category` para agregar una columna adicional que contenga un valor nulo: `'+UNION+SELECT+NULL,NULL--`

4. Continuamos agregando valores nulos hasta que desaparezca el error y la respuesta incluya contenido adicional que contenga los valores nulos.

![Pasted image 20230626163753](Pasted%20image%2020230626163753.png)

## Notas adicionales:

### Unión:
El operador de Unión combina los resultados de dos o más consultas dando lugar a la creación de un único conjunto de resultados que incluye todas las filas que pertenecen a todas las consultas en la Unión. En esta operación, combina dos consultas más y elimina los duplicados.

## Referencias:
- https://portswigger.net/web-security/sql-injection/union-attacks
- https://www.sqlshack.com/es/revision-ejemplos-y-uso-de-sql-union/#:~:text=El%20operador%20UNION%20combina%20los,filas%20y%20mantiene%20los%20duplicados.