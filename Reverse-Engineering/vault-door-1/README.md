# Vault Door 1

## Description
This challenge provides the Java source code for a vault. The password is verified by checking characters at specific positions using `password.charAt()`. The goal is to reconstruct the correct password.

## Approach
- Examined the Java source code.
- Located the `checkPassword()` method.
- Mapped each `password.charAt(index)` check to its corresponding character.
- Reconstructed the password by placing each character at its correct index.
- Ran the program with the reconstructed password to verify it and obtain the flag.

## Commands Used
```bash
file VaultDoor1.java
nano VaultDoor1.java
javac VaultDoor1.java
java VaultDoor1
```

## What I Learned
- Java validates strings character-by-character using `charAt()`.
- Character position checks can be reversed to reconstruct the original password.
- Repetitive reconstruction tasks can be automated with a small script instead of doing them manually.