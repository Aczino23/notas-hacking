#  caesar

## Descripción: 
Decrypt this [message](https://jupiter.challenges.picoctf.org/static/49f31c8f17817dc2d367428c9e5ab0bc/ciphertext).

**Pistas:**
1. caesar cipher [tutorial](https://learncryptography.com/classical-encryption/caesar-cipher)

## Solución:
1. Para este reto se nos da una cadena de texto:

```txt
picoCTF{ynkooejcpdanqxeykjrbdofgkq}
```

2. El código cifrado anterior se puede descifrar en línea usando el [Caesar-Cipher](https://www.dcode.fr/caesar-cipher) .. Brute Force Attack se puede aplicar para adivinar todas las combinaciones posibles para el cambio de la letra.

### Flag: picoCTF{crossingtherubiconvfhsjkou}

## Notas adicionales:

**El cifrado César (o código César)** es un cifrado de sustitución monoalfabético, donde cada letra se reemplaza por otra letra ubicada un poco más adelante en el alfabeto (por lo tanto, desplazada pero siempre igual para el mensaje cifrado dado). La distancia de desplazamiento se elige mediante un número llamado desplazamiento, que puede ser a la derecha (A a B) o a la izquierda (B a A).

## Referencias:
- https://privacycanada.net/classical-encryption/caesar-cipher/