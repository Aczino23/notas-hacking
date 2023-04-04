# tunn3l v1s10n

## Descripción: 
We found this [file](https://mercury.picoctf.net/static/7b2d7c26630e977197022d0af09e3aeb/tunn3l_v1s10n). Recover the flag.

**Pistas:**
1. Weird that it won't display right...

## Solución:
1. En este reto se nos da un archivo de tipo **data**:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/tunn3l_v1s10n]
└─$ ls
tunn3l_v1s10n
                                                                                                   
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/tunn3l_v1s10n]
└─$ file tunn3l_v1s10n
tunn3l_v1s10n: data
                                                                                                   
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/tunn3l_v1s10n]
└─$ xxd tunn3l_v1s10n| head
00000000: 424d 8e26 2c00 0000 0000 bad0 0000 bad0  BM.&,...........
00000010: 0000 6e04 0000 3201 0000 0100 1800 0000  ..n...2.........
00000020: 0000 5826 2c00 2516 0000 2516 0000 0000  ..X&,.%...%.....
00000030: 0000 0000 0000 231a 1727 1e1b 2920 1d2a  ......#..'..) .*
00000040: 211e 261d 1a31 2825 352c 2933 2a27 382f  !.&..1(%5,)3*'8/
00000050: 2c2f 2623 332a 262d 2420 3b32 2e32 2925  ,/&#3*&-$ ;2.2)%
00000060: 3027 2333 2a26 382c 2836 2b27 392d 2b2f  0'#3*&8,(6+'9-+/
00000070: 2623 1d12 0e23 1711 2916 0e55 3d31 9776  &#...#..)..U=1.v
00000080: 668b 6652 996d 569e 7058 9e6f 549c 6f54  f.fR.mV.pX.oT.oT
00000090: ab7e 63ba 8c6d bd8a 69c8 9771 c193 71c1  .~c..m..i..q..q.
                                                                                                   
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/tunn3l_v1s10n]
└─$ 
```

![Pasted image 20230404140429](Pasted%20image%2020230404140429.png)

2. Al parecer no podemos ver la flag: 

![Pasted image 20230404141104](Pasted%20image%2020230404141104.png)

3. Modificamos el alto de la imagen para poder visualizar la flag:

![Pasted image 20230404141442](Pasted%20image%2020230404141442.png)

![Pasted image 20230404141616](Pasted%20image%2020230404141616.png)

### Flag: picoCTF{qu1t3_a_v13w_2020}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| hexeditor | Es un editor de archivos binarios confiable y muy fácil de usar. Este visor hexadecimal de Linux se presenta con muchas opciones, por ejemplo, búsqueda / comparación rápida, resaltador, EBCDIC, esquemas de color, ajuste automático, modos INS / OVR, marcadores, seguimiento de cambios. Su cambiador de pantalla tiene más de setenta propiedades como fechas, flotantes, enteros y muchos más. |

## Referencias:
- https://en.wikipedia.org/wiki/List_of_file_signatures