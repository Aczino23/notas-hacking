# GDB Test Drive

## Descripción: 
Can you get the flag?Download this [binary](https://artifacts.picoctf.net/c/85/gdbme).Here's the test drive instructions:

-   `$ chmod +x gdbme`
-   `$ gdb gdbme`
-   `(gdb) layout asm`
-   `(gdb) break *(main+99)`
-   `(gdb) run`
-   `(gdb) jump *(main+104)`

**Pistas:**
- no pistas. 

## Solución:
1. En este reto se nos da un archivo que al parecer es un ejecutable: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDBTestDrive]
└─$ ls    
gdbme
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDBTestDrive]
└─$ file gdbme         
gdbme: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=eeea2c770465e109c185011ad3a7925a2796ce92, for GNU/Linux 3.2.0, not stripped
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDBTestDrive]
└─$ 
```

2. Le damos permisos de ejecución y ejecutamos el archivo y vemos que no hace nada:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDBTestDrive]
└─$ chmod +x gdbme
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDBTestDrive]
└─$ ls -la        
total 28
drwxr-xr-x  2 kali kali  4096 may 11 20:20 .
drwxr-xr-x 14 kali kali  4096 may 11 20:20 ..
-rwxr-xr-x  1 kali kali 17048 mar 15 23:15 gdbme
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDBTestDrive]
└─$ ./gdbme       
^C
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDBTestDrive]
└─$ 


```

3. Hacemos un debug al script para obtener la flag:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDBTestDrive]
└─$ gdb gdbme         
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
Reading symbols from gdbme...
(No debugging symbols found in gdbme)
(gdb) disassemble main
Dump of assembler code for function main:
   0x00000000000012c7 <+0>:     endbr64
   0x00000000000012cb <+4>:     push   %rbp
   0x00000000000012cc <+5>:     mov    %rsp,%rbp
   0x00000000000012cf <+8>:     sub    $0x50,%rsp
   0x00000000000012d3 <+12>:    mov    %edi,-0x44(%rbp)
   0x00000000000012d6 <+15>:    mov    %rsi,-0x50(%rbp)
   0x00000000000012da <+19>:    mov    %fs:0x28,%rax
   0x00000000000012e3 <+28>:    mov    %rax,-0x8(%rbp)
   0x00000000000012e7 <+32>:    xor    %eax,%eax
   0x00000000000012e9 <+34>:    movabs $0x4c75257240343a41,%rax
   0x00000000000012f3 <+44>:    movabs $0x4362383846336235,%rdx
   0x00000000000012fd <+54>:    mov    %rax,-0x30(%rbp)
   0x0000000000001301 <+58>:    mov    %rdx,-0x28(%rbp)
   0x0000000000001305 <+62>:    movabs $0x6030624760433530,%rax
   0x000000000000130f <+72>:    movabs $0x4e32676662346668,%rdx
   0x0000000000001319 <+82>:    mov    %rax,-0x20(%rbp)
   0x000000000000131d <+86>:    mov    %rdx,-0x18(%rbp)
   0x0000000000001321 <+90>:    movb   $0x0,-0x10(%rbp)
   0x0000000000001325 <+94>:    mov    $0x186a0,%edi
   0x000000000000132a <+99>:    call   0x1110 <sleep@plt>
--Type <RET> for more, q to quit, c to continue without paging--
   0x000000000000132f <+104>:   lea    -0x30(%rbp),%rax
   0x0000000000001333 <+108>:   mov    %rax,%rsi
   0x0000000000001336 <+111>:   mov    $0x0,%edi
   0x000000000000133b <+116>:   call   0x1209 <rotate_encrypt>
   0x0000000000001340 <+121>:   mov    %rax,-0x38(%rbp)
   0x0000000000001344 <+125>:   mov    0x2cc5(%rip),%rdx        # 0x4010 <stdout@@GLIBC_2.2.5>
   0x000000000000134b <+132>:   mov    -0x38(%rbp),%rax
   0x000000000000134f <+136>:   mov    %rdx,%rsi
   0x0000000000001352 <+139>:   mov    %rax,%rdi
   0x0000000000001355 <+142>:   call   0x10f0 <fputs@plt>
   0x000000000000135a <+147>:   mov    $0xa,%edi
   0x000000000000135f <+152>:   call   0x10c0 <putchar@plt>
   0x0000000000001364 <+157>:   mov    -0x38(%rbp),%rax
   0x0000000000001368 <+161>:   mov    %rax,%rdi
   0x000000000000136b <+164>:   call   0x10b0 <free@plt>
   0x0000000000001370 <+169>:   mov    $0x0,%eax
   0x0000000000001375 <+174>:   mov    -0x8(%rbp),%rcx
   0x0000000000001379 <+178>:   xor    %fs:0x28,%rcx
   0x0000000000001382 <+187>:   je     0x1389 <main+194>
   0x0000000000001384 <+189>:   call   0x10e0 <__stack_chk_fail@plt>
--Type <RET> for more, q to quit, c to continue without paging--
   0x0000000000001389 <+194>:   leave
   0x000000000000138a <+195>:   ret
End of assembler dump.
(gdb) break * (main+99)
Breakpoint 1 at 0x132a
(gdb) run
Starting program: /home/kali/picoCTF-Practice/reversing/GDBTestDrive/gdbme 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x000055555555532a in main ()
(gdb) jump *(main+104)
Continuing at 0x55555555532f.
picoCTF{d3bugg3r_dr1v3_197c378a}
[Inferior 1 (process 23390) exited normally]
(gdb) exit

┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/GDBTestDrive]
└─$ 
```

### Flag: picoCTF{d3bugg3r_dr1v3_197c378a}

## Notas adicionales:

### GNU Debugger:

GDB o GNU Debugger es el depurador estándar para el compilador GNU.
Es un depurador portable que se puede utilizar en varias plataformas Unix y funciona para varios lenguajes de programación como C, C++ y Fortran. GDB fue escrito por Richard Stallman en 1986. GDB es software libre distribuido bajo la licencia GPL.
GDB ofrece la posibilidad de trazar y modificar la ejecución de un programa. El usuario puede controlar y alterar los valores de las variables internas del programa.
GDB no contiene su propia interfaz gráfica de usuario y por defecto se controla mediante una interfaz de línea de comandos. Existen diversos front-ends que han sido diseñados para GDB, como Data Display Debugger, GDBtk/Insight y el «modo GUD» en Emacs.

## Referencias:
- https://www.sourceware.org/gdb/documentation/
- https://en.wikipedia.org/wiki/GNU_Debugger