# Safe Opener 2

## Descripción: 
What can you do with this file?I forgot the key to my safe but this [file](https://artifacts.picoctf.net/c/290/SafeOpener.class) is supposed to help me with retrieving the lost key. Can you help me unlock my safe?

**Pistas:**
1. Download and try to decompile the file.

## Solución:
 1. Para poder resolver este reto se nos da un archivo  `safeOpener.class`.

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/SafeOpener_2]
└─$ ls
SafeOpener.class
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/SafeOpener_2]
└─$ file SafeOpener.class 
SafeOpener.class: compiled Java class data, version 52.0 (Java 1.8)
                                                                                              
┌──(kali㉿kali)-[~/picoCTF-Practice/reversing/SafeOpener_2]
└─$
```

2. Como el archivo es `.class`, no se puede visualizar el código, por lo que con la pagina [javadecompilers.com](http://www.javadecompilers.com/) descompilaremos él archivo .class para visualizar el código.

3. Analizando el código dado, podemos ver que el código muestra directamente la flag sin necesitar de ejecutarlo.

```java
import java.io.IOException;
import java.util.Base64;
import java.io.Reader;
import java.io.BufferedReader;
import java.io.InputStreamReader;

// // Decompiled by Procyon v0.5.36
// public class SafeOpener
{
    public static void main(final String[] args) throws IOException {
        final BufferedReader keyboard = new BufferedReader(new InputStreamReader(System.in));
        final Base64.Encoder encoder = Base64.getEncoder();
        String encodedkey = "";
        String key = "";
        for (int i = 0; i < 3; ++i) {
            System.out.print("Enter password for the safe: ");
            key = keyboard.readLine();
            encodedkey = encoder.encodeToString(key.getBytes());
            System.out.println(encodedkey);
            final boolean isOpen = openSafe(encodedkey);
            if (isOpen) {
                break;
            }
            System.out.println("You have  " + (2 - i) + " attempt(s) left");
        }
    }
    
    public static boolean openSafe(final String password) {
        final String encodedkey = "picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_7db9fb8c}";
        if (password.equals(encodedkey)) {
            System.out.println("Sesame open");
            return true;
        }
        System.out.println("Password is incorrect\n");
        return false;
    }
}
```

### Flag: picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_7db9fb8c}

## Notas adicionales:

## Referencias:
- http://www.javadecompilers.com/