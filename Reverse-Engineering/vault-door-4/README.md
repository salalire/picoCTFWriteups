# Vault Door 4

## Description
This challenge stores the password as a byte array using decimal, hexadecimal, octal, and character literals. The goal is to recover the original password.

## Approach
- Examined the `checkPassword()` method.
- Observed that the password was stored directly in the `myBytes` array.
- Modified the program to print the byte array as a string using `new String(myBytes)`.
- Compiled and executed the modified program to reveal the password.
- Used the recovered password to unlock the vault.

## Commands Used
```bash
file VaultDoor4.java
nano VaultDoor4.java
javac VaultDoor4.java
java VaultDoor4
```

## What I Learned
- Java byte arrays can be converted directly into strings.
- The same ASCII character can be represented in decimal, hexadecimal, octal, or character literal form.
- Modifying a program to reveal internal data is an effective reverse engineering technique.
## Flag
picoCTF{jU5t_4_bUnCh_0f_bYt3s_759600abc3}