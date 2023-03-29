## Descripción: 
Decode this [message](https://jupiter.challenges.picoctf.org/static/14393e18d98fedbaedbc28896d7ef31a/message.wav) from the moon.

**Pistas:**
1. How did pictures from the moon landing get sent back to Earth?
2. What is the CMU mascot?, that might help select a RX option

## Solución:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/m00nwalk]
└─$ ls
message.wav
                                                                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/m00nwalk]
└─$ file message.wav
message.wav: RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 48000 Hz
                                                                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/m00nwalk]
└─$ sstv -d message.wav -o flag.png
[sstv] Searching for calibration header... Found!    
[sstv] Detected SSTV mode Scottie 1
[sstv] Decoding image...    [####################################################################################################] 100%
[sstv] Drawing image data...
[sstv] ...Done!
                                                                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/m00nwalk]
└─$ ls
flag.png  message.wav
                                                                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/m00nwalk]
└─$ open flag.png
                                                                                                                                       
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/m00nwalk]
└─$ 
```

![Pasted image 20230325151203](Pasted%20image%2020230325151203.png)

### Flag: picoCTF{beep_boop_im_in_space}

## Notas adicionales:
| Comando | Descripción |
| --- | --- |
| sstv | Un decodificador de televisión de escaneo lento de línea de comando que funciona con archivos de audio en lugar de leer una tarjeta de sonido (como la mayoría de los otros decodificadores). |

## Referencias:
- https://en.wikipedia.org/wiki/Apollo_11_missing_tapes
- https://github.com/colaclanth/sstv