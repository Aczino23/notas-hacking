# ASCII FTW

## Descripción: 
This program has constructed the flag using hex ascii values. Identify the flag text by disassembling the program.You can download the file from [here](https://artifacts.picoctf.net/c/508/asciiftw).

**Pistas:**
1. The combined range of hex-ascii for English alphabets and numerical digits is from 30 to 7A.
2. Online hex-ascii converters can be helpful.

## Solución:
1. En este reto se nos da un archivo binario:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/ASCII_FTW]
└─$ ls
asciiftw
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/ASCII_FTW]
└─$ chmod +x asciiftw
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/ASCII_FTW]
└─$ ls -la
total 28
drwxr-xr-x  2 kali kali  4096 may 22 19:21 .
drwxr-xr-x 17 kali kali  4096 may 22 19:21 ..
-rwxr-xr-x  1 kali kali 16752 may  9 18:17 asciiftw
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/ASCII_FTW]
└─$ ./asciiftw
The flag starts with 70
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/ASCII_FTW]
└─$
```

2. Para resolver este reto, debemos desensamblar el código, debido a que el archivo que nos dan es un ejecutable (un binario). Yo utilice el programa `ghidra`.

3. Ya teniendo el código desensamblado, podemos empezar a analizar el código ensamblador, un recordatorio muy importante es que la bandera empieza con el valor hexadecimal 70 ('p').

4. Encontramos en la función main lo siguiente:

```bash
        00101184 c6 45 d0 70     MOV        byte ptr [RBP + local_38],0x70
        00101188 c6 45 d1 69     MOV        byte ptr [RBP + local_37],0x69
        0010118c c6 45 d2 63     MOV        byte ptr [RBP + local_36],0x63
        00101190 c6 45 d3 6f     MOV        byte ptr [RBP + local_35],0x6f
        00101194 c6 45 d4 43     MOV        byte ptr [RBP + local_34],0x43
        00101198 c6 45 d5 54     MOV        byte ptr [RBP + local_33],0x54
        0010119c c6 45 d6 46     MOV        byte ptr [RBP + local_32],0x46
        001011a0 c6 45 d7 7b     MOV        byte ptr [RBP + local_31],0x7b
        001011a4 c6 45 d8 41     MOV        byte ptr [RBP + local_30],0x41
        001011a8 c6 45 d9 53     MOV        byte ptr [RBP + local_2f],0x53
        001011ac c6 45 da 43     MOV        byte ptr [RBP + local_2e],0x43
        001011b0 c6 45 db 49     MOV        byte ptr [RBP + local_2d],0x49
        001011b4 c6 45 dc 49     MOV        byte ptr [RBP + local_2c],0x49
        001011b8 c6 45 dd 5f     MOV        byte ptr [RBP + local_2b],0x5f
        001011bc c6 45 de 49     MOV        byte ptr [RBP + local_2a],0x49
        001011c0 c6 45 df 53     MOV        byte ptr [RBP + local_29],0x53
        001011c4 c6 45 e0 5f     MOV        byte ptr [RBP + local_28],0x5f
        001011c8 c6 45 e1 45     MOV        byte ptr [RBP + local_27],0x45
        001011cc c6 45 e2 41     MOV        byte ptr [RBP + local_26],0x41
        001011d0 c6 45 e3 53     MOV        byte ptr [RBP + local_25],0x53
        001011d4 c6 45 e4 59     MOV        byte ptr [RBP + local_24],0x59
        001011d8 c6 45 e5 5f     MOV        byte ptr [RBP + local_23],0x5f
        001011dc c6 45 e6 38     MOV        byte ptr [RBP + local_22],0x38
        001011e0 c6 45 e7 39     MOV        byte ptr [RBP + local_21],0x39
        001011e4 c6 45 e8 36     MOV        byte ptr [RBP + local_20],0x36
        001011e8 c6 45 e9 30     MOV        byte ptr [RBP + local_1f],0x30
        001011ec c6 45 ea 46     MOV        byte ptr [RBP + local_1e],0x46
        001011f0 c6 45 eb 30     MOV        byte ptr [RBP + local_1d],0x30
        001011f4 c6 45 ec 41     MOV        byte ptr [RBP + local_1c],0x41
        001011f8 c6 45 ed 46     MOV        byte ptr [RBP + local_1b],0x46
        001011fc c6 45 ee 7d     MOV        byte ptr [RBP + local_1a],0x7d

```

5. Si solo tomamos los valores hexadecimales, tenemos la cadena:

```txt
70 69 63 6f 43 54 46 7b 41 53 43 49 49 5f 49 53 5f 45 41 53 59 5f 38 39 36 30 46 30 41 46 7d
```

6. Utilizaremos [rapidtables](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html) para transformar de HEX a ASCII y obtenemos la flag:

### Flag: picoCTF{ASCII_IS_EASY_8960F0AF}

## Notas adicionales:

### Ghidra:
**GHIDRA** es un marco de trabajo de ingeniería inversa de software (SRE) que ayuda a analizar código malicioso y malware como virus. Ha sido creado y mantenido por la Dirección de Investigación de la Agencia Nacional de Seguridad. Ahora bien, si eso suena un poco aterrador, esta herramienta no se está instalando en sus dispositivos. Ha sido desarrollado para luchar contra el malware y los virus para que puedan ser detenidos. Este post ofrece una visión general de la herramienta de ingeniería inversa GHIDRA de NSA.

## Referencias:
- https://www.rapidtables.com/convert/number/hex-to-ascii.html