# Secrets

## Descripción: 
We have several pages hidden. Can you find the one with the flag?The website is running [here](http://saturn.picoctf.net:53932/).

**Pistas:**
1. folders folders folders

## Solución:
1. Se nos proporciona la siguiente pagina web:

![Pasted image 20230427124243](Pasted%20image%2020230427124243.png)

2. Si navegamos al suburl secret http://saturn.picoctf.net/secret/, encontramos un sitio web que dice "Finalmente. Casi me encontraste. Lo estás haciendo bien". Vamos por buen camino.

3.  Si repetimos el mismo proceso que antes, encontramos que hay otra carpeta con un nombre sospechoso, "hidden", por lo que navegamos a [http://saturn.picoctf.net:54925/secret/hidden/](http://saturn.picoctf.net:54925/secret/hidden/).

4. Seguimos repitiendo este proceso hasta que llegamos a un sitio web que dice "Finalmente. Me encontraste. Pero puedes verme". La bandera probablemente esté oculta por el css. Solo podemos mirar el HTML fuente para obtener la bandera.

### Flag: picoCTF{succ3ss_@h3n1c@10n_790d2615}

## Notas adicionales:

## Referencias: