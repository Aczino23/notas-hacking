## Objetivo:
Can you invoke help flags for a tool or binary? [This program](https://mercury.picoctf.net/static/f95b1ee9f29d631d99073e34703a2826/warm) has extraordinarily helpful information...

**Hints:**
1. This program will only work in the webshell or another Linux computer.
2. To get the file accessible in your shell, enter the following in the Terminal prompt: `$ wget https://mercury.picoctf.net/static/f95b1ee9f29d631d99073e34703a2826/warm`
3. Run this program by entering the following in the Terminal prompt: `$ ./warm`, but you'll first have to make it executable with `$ chmod +x warm`
4. -h and --help are the most common arguments to give to programs to get more information from them!
5. Not every program implements help features like -h and --help.

## Solución:

```bash
┌──(kali㉿kali)-[~/picoCTF/generalSkills/Wave_a_flag]
└─$ ls -l
total 12
-rw-r--r-- 1 kali kali 10936 mar 15  2021 warm
                                                                                     
┌──(kali㉿kali)-[~/picoCTF/generalSkills/Wave_a_flag]
└─$ chmod +x warm
                                                                            
┌──(kali㉿kali)-[~/picoCTF/generalSkills/Wave_a_flag]
└─$ ls -l        
total 12
-rwxr-xr-x 1 kali kali 10936 mar 15  2021 warm
                                                                                        
┌──(kali㉿kali)-[~/picoCTF/generalSkills/Wave_a_flag]
└─$ ./warm -h
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_f0668f62}
                                                                                       
┌──(kali㉿kali)-[~/picoCTF/generalSkills/Wave_a_flag]
└─$ 
```

### **flag:** picoCTF{b1scu1ts_4nd_gr4vy_f0668f62}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| chmod | gestionar los permisos de archivos y directorios dentro del sistema |

## Referencias:
- https://bioinf.comav.upv.es/courses/unix/scripts_bash.html
- https://computernewage.com/2019/01/13/scripting-linux-bash-crear-ejecutar-script/