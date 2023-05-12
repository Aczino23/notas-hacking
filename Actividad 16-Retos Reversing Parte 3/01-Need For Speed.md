# Need For Speed

## Descripción: 
The name of the game is [speed](https://www.youtube.com/watch?v=8piqd2BWeGI). Are you quick enough to solve this problem and keep it above 50 mph? [need-for-speed](https://jupiter.challenges.picoctf.org/static/27dd5548b14661f65ce3ac6a8a8f575b/need-for-speed).

**Pistas:**
1. What is the final key?

## Solución:
1. En este reto se nos da un archivo que al parecer es un ejecutable: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/NeedForSpeed]
└─$ ls
need-for-speed
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/NeedForSpeed]
└─$ file need-for-speed                   
need-for-speed: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=2d0d401d07683664113690a7fb94413a0039d228, not stripped
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/NeedForSpeed]
└─$ 
```

2. Le damos permisos de ejecución y ejecutamos el archivo: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/NeedForSpeed]
└─$ chmod +x need-for-speed 
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/NeedForSpeed]
└─$ ls -la
total 20
drwxr-xr-x  2 kali kali 4096 may 11 19:11 .
drwxr-xr-x 13 kali kali 4096 may 11 19:11 ..
-rwxr-xr-x  1 kali kali 8888 oct 26  2020 need-for-speed
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/NeedForSpeed]
└─$ ./need-for-speed 
Keep this thing over 50 mph!
============================

Creating key...
Not fast enough. BOOM!
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/NeedForSpeed]
└─$
```

3. Hacemos un debug al script: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/NeedForSpeed]
└─$ gdb need-for-speed 
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
Reading symbols from need-for-speed...
(No debugging symbols found in need-for-speed)
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x00000000000005d8  _init
0x0000000000000600  putchar@plt
0x0000000000000610  puts@plt
0x0000000000000620  alarm@plt
0x0000000000000630  __sysv_signal@plt
0x0000000000000640  exit@plt
0x0000000000000650  __cxa_finalize@plt
0x0000000000000660  _start
0x0000000000000690  deregister_tm_clones
0x00000000000006d0  register_tm_clones
0x0000000000000720  __do_global_dtors_aux
0x0000000000000760  frame_dummy
0x000000000000076a  decrypt_flag
0x00000000000007f1  calculate_key
0x000000000000080e  alarm_handler
0x000000000000082f  set_timer
0x000000000000087d  get_key
0x00000000000008ac  print_flag
--Type <RET> for more, q to quit, c to continue without paging--
0x00000000000008d8  header
0x000000000000091a  main
0x0000000000000960  __libc_csu_init
0x00000000000009d0  __libc_csu_fini
0x00000000000009d4  _fini
(gdb) 
(gdb) 
(gdb) set disassembly-flavor intel
(gdb) disassemble main
Dump of assembler code for function main:
   0x000000000000091a <+0>:     push   rbp
   0x000000000000091b <+1>:     mov    rbp,rsp
   0x000000000000091e <+4>:     sub    rsp,0x10
   0x0000000000000922 <+8>:     mov    DWORD PTR [rbp-0x4],edi
   0x0000000000000925 <+11>:    mov    QWORD PTR [rbp-0x10],rsi
   0x0000000000000929 <+15>:    mov    eax,0x0
   0x000000000000092e <+20>:    call   0x8d8 <header>
   0x0000000000000933 <+25>:    mov    eax,0x0
   0x0000000000000938 <+30>:    call   0x82f <set_timer>
   0x000000000000093d <+35>:    mov    eax,0x0
   0x0000000000000942 <+40>:    call   0x87d <get_key>
   0x0000000000000947 <+45>:    mov    eax,0x0
   0x000000000000094c <+50>:    call   0x8ac <print_flag>
   0x0000000000000951 <+55>:    mov    eax,0x0
   0x0000000000000956 <+60>:    leave
   0x0000000000000957 <+61>:    ret
End of assembler dump.
(gdb) break main
Breakpoint 1 at 0x91e
(gdb) info breakpoints
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x000000000000091e <main+4>
(gdb) run
Starting program: /home/kali/picoCTF-Practice/reversing/NeedForSpeed/need-for-speed 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x000055555540091e in main ()
(gdb) disassemble main
Dump of assembler code for function main:
   0x000055555540091a <+0>:     push   rbp
   0x000055555540091b <+1>:     mov    rbp,rsp
=> 0x000055555540091e <+4>:     sub    rsp,0x10
   0x0000555555400922 <+8>:     mov    DWORD PTR [rbp-0x4],edi
   0x0000555555400925 <+11>:    mov    QWORD PTR [rbp-0x10],rsi
   0x0000555555400929 <+15>:    mov    eax,0x0
   0x000055555540092e <+20>:    call   0x5555554008d8 <header>
   0x0000555555400933 <+25>:    mov    eax,0x0
   0x0000555555400938 <+30>:    call   0x55555540082f <set_timer>
   0x000055555540093d <+35>:    mov    eax,0x0
   0x0000555555400942 <+40>:    call   0x55555540087d <get_key>
   0x0000555555400947 <+45>:    mov    eax,0x0
   0x000055555540094c <+50>:    call   0x5555554008ac <print_flag>
   0x0000555555400951 <+55>:    mov    eax,0x0
   0x0000555555400956 <+60>:    leave
   0x0000555555400957 <+61>:    ret
End of assembler dump.
(gdb) call (int) get_key()
Creating key...
Finished
$1 = 9
(gdb) call (int) print_flag()
Printing flag:
PICOCTF{Good job keeping bus #1f2ac4ec speeding along!}
$2 = 56
(gdb)
```

### Flag: PICOCTF{Good job keeping bus # 1f2ac4ec speeding along!}

## Notas adicionales:

### GNU Debugger:

GDB o GNU Debugger es el depurador estándar para el compilador GNU.
Es un depurador portable que se puede utilizar en varias plataformas Unix y funciona para varios lenguajes de programación como C, C++ y Fortran. GDB fue escrito por Richard Stallman en 1986. GDB es software libre distribuido bajo la licencia GPL.
GDB ofrece la posibilidad de trazar y modificar la ejecución de un programa. El usuario puede controlar y alterar los valores de las variables internas del programa.
GDB no contiene su propia interfaz gráfica de usuario y por defecto se controla mediante una interfaz de línea de comandos. Existen diversos front-ends que han sido diseñados para GDB, como Data Display Debugger, GDBtk/Insight y el «modo GUD» en Emacs.

## Referencias:
- https://www.sourceware.org/gdb/documentation/
- https://en.wikipedia.org/wiki/GNU_Debugger