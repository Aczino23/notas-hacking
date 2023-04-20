# waves over lambda

## Descripción: 
We made a lot of substitutions to encrypt this. Can you decrypt it? Connect with `nc jupiter.challenges.picoctf.org 13758`.

**Pistas:**
1. Flag is not in the usual flag format

## Solución:
1. El texto cifrado proporcionado se muestra a continuación. Aparentemente está codificado por encriptación de cifrado de sustitución. Para resolver esto, se puede utilizar fácilmente la fuerza bruta.

```bash
┌──(kali㉿kali)-[~]
└─$ nc jupiter.challenges.picoctf.org 13758 
-------------------------------------------------------------------------------
rovnfhcs tlfl bs eomf gphn - gflzmlvre_bs_r_oqlf_phyxdh_dvqcgfchem
-------------------------------------------------------------------------------
al alfl voc ymrt yofl cthv h zmhfclf og hv tomf omc og omf stbu cbpp al sha tlf sbvj, hvd ctlv b mvdlfscood gof ctl gbfsc cbyl athc ahs ylhvc xe h stbu gomvdlfbvn bv ctl slh.  b ymsc hrjvoapldnl b thd thfdpe lels co pooj mu atlv ctl slhylv copd yl stl ahs sbvjbvn; gof gfoy ctl yoylvc cthc ctle fhctlf umc yl bvco ctl xohc cthv cthc b ybntc xl shbd co no bv, ye tlhfc ahs, hs bc alfl, dlhd abctbv yl, uhfcpe abct gfbntc, uhfcpe abct toffof og ybvd, hvd ctl ctomntcs og athc ahs elc xlgofl yl.

┌──(kali㉿kali)-[~]
└─$
```

2. Usando la herramienta https://planetcalc.com/8047/ desciframos el mensaje y obtenemos la bandera:

```txt
------------------------------------------------------------------------------- CONGRATS HERE IS YOUR FLAG - FREQUENCY_IS_C_OVER_LAMBDA_DNVTFRTAYU ------------------------------------------------------------------------------- WE WERE NOT MUCH MORE THAN A QUARTER OF AN HOUR OUT OF OUR SHIP TILL WE SAW HER SINK, AND THEN I UNDERSTOOD FOR THE FIRST TIME WHAT WAS MEANT BY A SHIP FOUNDERING IN THE SEA. I MUST ACKNOWLEDGE I HAD HARDLY EYES TO LOOK UP WHEN THE SEAMEN TOLD ME SHE WAS SINKING; FOR FROM THE MOMENT THAT THEY RATHER PUT ME INTO THE BOAT THAN THAT I MIGHT BE SAID TO GO IN, MY HEART WAS, AS IT WERE, DEAD WITHIN ME, PARTLY WITH FRIGHT, PARTLY WITH HORROR OF MIND, AND THE THOUGHTS OF WHAT WAS YET BEFORE ME.
```

**Nota:** La bandera no tiene el formato habitual. 

### Flag: FREQUENCY_IS_C_OVER_LAMBDA_DNVTFRTAYU

## Notas adicionales:

## Cifrado de sustitución:
En criptografía, un **cifrado de sustitución** es un método de cifrado en el que las unidades de texto plano se reemplazan con el texto cifrado, de manera definida, con la ayuda de una clave; las "unidades" pueden ser letras sueltas (las más comunes), pares de letras, trillizos de letras, mezclas de las anteriores, etc. El receptor descifra el texto realizando el proceso de sustitución inversa para extraer el mensaje original.

## Referencias:
- https://es.wikipedia.org/wiki/Cifrado_por_sustituci%C3%B3n
- https://planetcalc.com/8047/