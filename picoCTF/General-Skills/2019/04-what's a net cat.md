## Objetivo:
Using netcat (nc) is going to be pretty important. Can you connect to `jupiter.challenges.picoctf.org` at port `25103` to get the flag?

**Hints:** nc [tutorial](https://linux.die.net/man/1/nc)

## Solución:

```bash
┌──(kali㉿kali)-[~]
└─$ nc jupiter.challenges.picoctf.org 25103
You're on your way to becoming the net cat master
picoCTF{nEtCat_Mast3ry_d0c64587}
                                                                                   
┌──(kali㉿kali)-[~]
└─$ 
```

### **flag:** picoCTF{nEtCat_Mast3ry_d0c64587

## Notas adicionales:
- El comando `nc` es un comando de sistemas Unix que se usa para llevar a cabo diversas tareas de red. Funciona en sistemas nix como Linux, BSD o macOS. Aunque el comando se usa abreviadamente como `nc`, su nombre completo es [Netcat](https://es.wikipedia.org/wiki/Netcat).

- La sintaxis básica del comando Netcat es: 

```bash
nc [opciones] HOST PUERTO
```

## Referencias:
- https://linux.die.net/man/1/nc