# picoCTF 2019 - Vault Door 8 Writeup

## Challenge Information

- **Challenge:** Vault Door 8
- **Category:** Reverse Engineering
- **Difficulty:** Hard
- **Platform:** picoCTF 2019

## Description

Apparently Dr. Evil's minions knew that our agency was making copies of their source code, because they intentionally sabotaged this source code in order to make it harder for our agents to analyze and crack into! The result is a quite mess, but I trust that my best special agent will find a way to solve it.

The source code for this vault is here: VaultDoor8.java

The important part of the source code is:

```java
char[] scrambled = scramble(password);

char[] expected = {
    0xF4, 0xC0, 0x97, 0xF0,
    ...
};

return Arrays.equals(scrambled, expected);
```

The goal is to recover the original password that produces the expected scrambled array.

---

## Challenge I Faced

At first, the source code looked intentionally confusing because of the unnecessary variables and comments.

The biggest challenge was understanding that the password itself was never encrypted. Instead, each character had its bits rearranged multiple times using the `switchBits()` function.

Once I understood that each operation only swaps two bits, I realized the transformation could be reversed.

---

## My Approach

The `scramble()` function performs the following sequence of bit swaps for every character:

```java
switchBits(c, 1, 2);
switchBits(c, 0, 3);
switchBits(c, 5, 6);
switchBits(c, 4, 7);
switchBits(c, 0, 1);
switchBits(c, 3, 4);
switchBits(c, 2, 5);
switchBits(c, 6, 7);
```

Since swapping two bits is its own inverse, the original password can be recovered by applying the same swaps **in the reverse order**.

The reverse sequence is:

```java
switchBits(c, 6, 7);
switchBits(c, 2, 5);
switchBits(c, 3, 4);
switchBits(c, 0, 1);
switchBits(c, 4, 7);
switchBits(c, 5, 6);
switchBits(c, 0, 3);
switchBits(c, 1, 2);
```

I copied the `expected` array from the source code and applied the reverse sequence to every character.

```java
char[] password = reverse(expected);
System.out.println(new String(password));
```

This reconstructed the original password.

---

## What I Learned

- Bit swapping is reversible.
- The inverse of multiple transformations is obtained by applying the same operations in the opposite order.
- Carefully reading the source code is often enough to solve reverse engineering challenges.
- Obfuscated code may look complicated, but identifying the core logic simplifies the problem significantly.
- Understanding bitwise operations (`<<`, `>>`, `&`, `|`) is essential for reverse engineering.

---

## Flag

```text
picoCTF{s0m3_m0r3_b1t_sh1fTiNg_bbb568cb7}
```