# GDB baby step 2

## Descripción:
Can you figure out what is in the `eax` register at the end of the `main` function? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`.Debug [this](https://artifacts.picoctf.net/c/520/debugger0_b).

**Pistas:**
1. You could calculate `eax` yourself, or you could set a breakpoint for after the calculcation and inspect `eax` to let the program do the heavy-lifting for you.

## Solución:
1. En este reto se nos da un archivo ejecutable, que al momento de ejecutarlo al parecer no realiza nada: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDB_baby_step_2]
└─$ ls
debugger0_b
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDB_baby_step_2]
└─$ file debugger0_b 
debugger0_b: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=95b0203be2982e75dbc01d1cc25b1309f7aec5f7, for GNU/Linux 3.2.0, not stripped
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDB_baby_step_2]
└─$ chmod +x debugger0_b 
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDB_baby_step_2]
└─$ ls -la
total 24
drwxr-xr-x  2 kali kali  4096 may 22 20:24 .
drwxr-xr-x 23 kali kali  4096 may 22 20:23 ..
-rwxr-xr-x  1 kali kali 16304 may  9 18:37 debugger0_b
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDB_baby_step_2]
└─$ ./debugger0_b 
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDB_baby_step_2]
└─$ 
```

2. Con ayuda de la herramienta `gdb` desembalamos el ejecutable: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDB_baby_step_2]
└─$ gdb debugger0_b 
GNU gdb (Debian 13.1-2) 13.1
Copyright (C) 2023 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_b...
(No debugging symbols found in debugger0_b)
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000401106 <+0>:     endbr64
   0x000000000040110a <+4>:     push   %rbp
   0x000000000040110b <+5>:     mov    %rsp,%rbp
   0x000000000040110e <+8>:     mov    %edi,-0x14(%rbp)
   0x0000000000401111 <+11>:    mov    %rsi,-0x20(%rbp)
   0x0000000000401115 <+15>:    movl   $0x1e0da,-0x4(%rbp)
   0x000000000040111c <+22>:    movl   $0x25f,-0xc(%rbp)
   0x0000000000401123 <+29>:    movl   $0x0,-0x8(%rbp)
   0x000000000040112a <+36>:    jmp    0x401136 <main+48>
   0x000000000040112c <+38>:    mov    -0x8(%rbp),%eax
   0x000000000040112f <+41>:    add    %eax,-0x4(%rbp)
   0x0000000000401132 <+44>:    addl   $0x1,-0x8(%rbp)
   0x0000000000401136 <+48>:    mov    -0x8(%rbp),%eax
   0x0000000000401139 <+51>:    cmp    -0xc(%rbp),%eax
   0x000000000040113c <+54>:    jl     0x40112c <main+38>
   0x000000000040113e <+56>:    mov    -0x4(%rbp),%eax
   0x0000000000401141 <+59>:    pop    %rbp
   0x0000000000401142 <+60>:    ret
End of assembler dump.
(gdb)
```



### Flag: 

## Notas adicionales:
| Comando | Descripción |
| --- | --- |

## Referencias: