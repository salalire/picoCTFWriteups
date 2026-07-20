# Vault Door 3

## Description
This challenge provides the Java source code for a vault. The password is transformed through several loops before being compared with a target string. The goal is to recover the original password.

## Approach
- Examined the `checkPassword()` method.
- Identified that the password was copied into a buffer using multiple loops before comparison.
- Modified the source code to print the contents of the buffer after it was constructed.
- Compiled and executed the modified program.
- Used the printed value to reconstruct the correct password and obtain the flag.

## Commands Used
```bash
file VaultDoor3.java
nano VaultDoor3.java
javac VaultDoor3.java
java VaultDoor3
```
## Flag
picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_e60bc2}
## What I Learned
- Programs can be modified to reveal intermediate values during execution.
- Printing internal variables is a useful reverse engineering technique when source code is available.
- Understanding how loops manipulate data is essential for reversing password transformations.