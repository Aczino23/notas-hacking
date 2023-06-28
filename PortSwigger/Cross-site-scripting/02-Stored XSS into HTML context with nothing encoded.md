# # Lab: Stored XSS into HTML context with nothing encoded

## Descripción: 
This lab contains a [stored cross-site scripting](https://portswigger.net/web-security/cross-site-scripting/stored) vulnerability in the comment functionality.
To solve this lab, submit a comment that calls the `alert` function when the blog post is viewed.

## Solución:
1. Ingresamos lo siguiente en el cuadro de comentarios:

```html
<script>alert(1)</script>
```

2. Ingresamos un nombre, correo electrónico y sitio web.

3. Hacemos clic en "Publicar comentario"..

![Pasted image 20230627141122](Pasted%20image%2020230627141122.png)

4. Volvemos al blog.
 
![Pasted image 20230627141155](Pasted%20image%2020230627141155.png)

![Pasted image 20230627141259](Pasted%20image%2020230627141259.png)

## Notas adicionales:

## Tipo de ataques XSS (Cross Site Scripting)

### 1. **XSS Reflejado**:
La secuencia de comandos reflejada entre sitios surge cuando una aplicación recibe datos maliciosos en una solicitud HTTP y los incluye dentro de la respuesta inmediata.
**Ejemplo**: Supongamos que un sitio web tiene una función de búsqueda (la cual no realiza ningún procesamiento de los datos) y el usuario proporciona un término en un parámetro de URL

### 2. **XSS Almacenado**:
Las secuencias de comandos almacenadas entre sitios (o XSS persistentes) surgen cuando una aplicación recibe datos de una fuente que no es de confianza y los incluye en sus respuestas HTTP posteriores.
**Ejemplo:** Supongamos que tenemos un sitio web en el que los usuarios pueden comentar los artículos de un blog. Estos comentarios se enviarán mediante una solicitud HTTP.
Suponiendo que la aplicación no realiza ningún otro procesamiento de los datos, un atacante podría crear una sentencia de código malicioso e insertarla (de forma encriptada) dentro de la solicitud. 
Para que la solicitud la guarde como un comentario en la base de datos.
Cualquier usuario que visite la publicación del blog ahora recibirá el script dentro de la respuesta de la aplicación.

### 3. **XSS Basado en DOM**
El XSS basado en DOM surge cuando una aplicación que tiene código JavaScript del lado del cliente procesa datos de una fuente maliciosa, generalmente escribiendo los datos en el DOM.
El atacante puede modificar el DOM utilizando código JavaScript añadiendo nuevas etiquetas, modificando o eliminando otras, cambiando sus atributos HTML, añadiendo clases, cambiando el contenido de texto, entre otras muchas acciones más, incluyendo la inserción de código malicioso.

## Referencias:
- https://blog.hackmetrix.com/xss-cross-site-scripting/