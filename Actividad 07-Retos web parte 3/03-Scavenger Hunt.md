## Descripción: 
There is some interesting information hidden around this site [http://mercury.picoctf.net:39698/](http://mercury.picoctf.net:39698/). Can you find it?

**Pistas:**
1. You should have enough hints to find the files, don't run a brute forcer.

## Solución:
1. Al inspeccionar el código fuente de la pagina en el archivo índice.html encontramos la primera parte de la bandera: 

```html
<!doctype html>
<html>
  <head>
    <title>Scavenger Hunt</title>
    <link href="https://fonts.googleapis.com/css?family=Open+Sans|Roboto" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="mycss.css">
    <script type="application/javascript" src="myjs.js"></script>
  </head>

  <body>
    <div class="container">
      <header>
		<h1>Just some boring HTML</h1>
      </header>

      <button class="tablink" onclick="openTab('tabintro', this, '#222')" id="defaultOpen">How</button>
      <button class="tablink" onclick="openTab('tababout', this, '#222')">What</button>

      <div id="tabintro" class="tabcontent">
		<h3>How</h3>
		<p>How do you like my website?</p>
      </div>

      <div id="tababout" class="tabcontent">
		<h3>What</h3>
		<p>I used these to make this site: <br/>
		  HTML <br/>
		  CSS <br/>
		  JS (JavaScript)
		</p>
	<!-- Here's the first part of the flag: picoCTF{t -->
      </div>

    </div>

  </body>
</html>

```

2. En la hoja de estilos de la pagina encortamos la segunda parte de la bandera: 

```css
div.container {
    width: 100%;
}

header {
    background-color: black;
    padding: 1em;
    color: white;
    clear: left;
    text-align: center;
}

body {
    font-family: Roboto;
}

h1 {
    color: white;
}

p {
    font-family: "Open Sans";
}

.tablink {
    background-color: #555;
    color: white;
    float: left;
    border: none;
    outline: none;
    cursor: pointer;
    padding: 14px 16px;
    font-size: 17px;
    width: 50%;
}

.tablink:hover {
    background-color: #777;
}

.tabcontent {
    color: #111;
    display: none;
    padding: 50px;
    text-align: center;
}

#tabintro { background-color: #ccc; }
#tababout { background-color: #ccc; }

/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */
```

3. En el archivo de los JavaScript de la pagina encontramos una pista la cual nos indica que ¿Cómo puedo evitar que Google indexe mi sitio web? esto nos suena a que la pagina puede tener un archivo robots.txt:

```javascript
function openTab(tabName,elmnt,color) {
    var i, tabcontent, tablinks;
    tabcontent = document.getElementsByClassName("tabcontent");
    for (i = 0; i < tabcontent.length; i++) {
	tabcontent[i].style.display = "none";
    }
    tablinks = document.getElementsByClassName("tablink");
    for (i = 0; i < tablinks.length; i++) {
	tablinks[i].style.backgroundColor = "";
    }
    document.getElementById(tabName).style.display = "block";
    if(elmnt.style != null) {
	elmnt.style.backgroundColor = color;
    }
}

window.onload = function() {
    openTab('tabintro', this, '#222');
}

/* How can I keep Google from indexing my website? */

```

4. Cuando vamos al la url http://mercury.picoctf.net:39698/robots.txt encontramos la tercera parte de la bandera y una pista la cual es: Creo que este es un servidor apache... ¿puedes acceder a la siguiente bandera?:

```txt
User-agent: *
Disallow: /index.html
# Part 3: t_0f_pl4c
# I think this is an apache server... can you Access the next flag?
```

5.  En base a la pista anterior vamos a http://mercury.picoctf.net:39698/.htaccess de la pagina y obtenemos la cuarta parte de la flag, además vemos que nos dejaron una pista:  Me encanta hacer sitios web en mi Mac, puedo almacenar mucha información allí.

```txt
# Part 4: 3s_2_lO0k
# I love making websites on my Mac, I can Store a lot of information there.
```

6. Vamos a http://mercury.picoctf.net:39698/.DS_Store para obtener la ultima parte de la flag.

```txt
Congrats! You completed the scavenger hunt. Part 5: _fa04427c}
```

### Flag: picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_fa04427c}

## Notas adicionales:

## Referencias:
- https://httpd.apache.org/docs/2.4/en/howto/htaccess.html
- https://en.wikipedia.org/wiki/.DS_Store