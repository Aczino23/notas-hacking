## Objetivo:
Python scripts are invoked kind of like programs in the Terminal... Can you run [this Python script](https://mercury.picoctf.net/static/325a52d249be0bd3811421eacd2c877a/ende.py) using [this password](https://mercury.picoctf.net/static/325a52d249be0bd3811421eacd2c877a/pw.txt) to get [the flag](https://mercury.picoctf.net/static/325a52d249be0bd3811421eacd2c877a/flag.txt.en)?

**Hints:** 
- Get the Python script accessible in your shell by entering the following command in the Terminal prompt: `$ wget https://mercury.picoctf.net/static/325a52d249be0bd3811421eacd2c877a/ende.py`
- $ man python

## Solución:

```bash
PS C:\Users\Cristian\Downloads> py .\ende.py -d .\flag.txt.en
Please enter the password:ac9bd0ffac9bd0ffac9bd0ffac9bd0ff
picoCTF{4p0110_1n_7h3_h0us3_ac9bd0ff}
PS C:\Users\Cristian\Downloads>
```

### **flag:** picoCTF{4p0110_1n_7h3_h0us3_ac9bd0ff}

## Notas adicionales:

 ### Python:
- Python es un lenguaje de programación interpretado cuya filosofía hace hincapié en una sintaxis que favorezca un código legible.

- Se trata de un lenguaje de programación multiparadigma, ya que soporta orientación a objetos, programación imperativa y, en menor medida, programación funcional. Es un lenguaje interpretado, usa tipado dinámico y es multiplataforma.

## Referencias:
- https://www.mclibre.org/consultar/python/otros/python-uso.html
