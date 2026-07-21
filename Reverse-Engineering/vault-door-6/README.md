# Vault Door 6

**Category:** Reverse Engineering  
**Difficulty:** Medium  
**Platform:** picoCTF

---

## Description

The goal of this challenge is to recover the vault password by analyzing the Java source code.

Unlike the previous challenge that used multiple encoding schemes, this vault protects the password using an **XOR operation**.

---

## Source Code Analysis

The important verification code is:

```java
for (int i=0; i<32; i++) {
    if (((passBytes[i] ^ 0x55) - myBytes[i]) != 0) {
        return false;
    }
}
```

This means the program performs:

```
password XOR 0x55
```

and compares the result with the values stored inside `myBytes`.

Therefore,

```
(password ^ 0x55) == myBytes
```

To recover the original password, we simply reverse the XOR operation.

Since XOR is reversible:

```
A ^ B = C

C ^ B = A
```

The original password can be recovered by:

```
password = myBytes ^ 0x55
```

---

## My Thought Process

I first analyzed the source code to understand how the password was being verified.

The hint mentioned that XOR can be reversed using the same key.

Instead of calculating each character manually, I wrote a small Java program that loops through every byte in `myBytes`, XORs it with `0x55`, and prints the resulting characters.

This immediately revealed the correct password.

---

## Solution

I wrote the following Java program:

```java
class Pf {
    public static void main(String[] args) {

        byte[] myBytes = {
            0x3b, 0x65, 0x21, 0xa , 0x38, 0x0 , 0x36, 0x1d,
            0xa , 0x3d, 0x61, 0x27, 0x11, 0x66, 0x27, 0xa ,
            0x21, 0x1d, 0x61, 0x3b, 0xa , 0x2d, 0x65, 0x27,
            0xa , 0x61, 0x37, 0x65, 0x61, 0x65, 0x65, 0x64
        };

        for(int i = 0; i < myBytes.length; i++) {
            System.out.print((char)(myBytes[i] ^ 0x55));
        }
    }
}
```

Running the program prints the vault password.

Submit it in the required format:

```
picoCTF{password}
```

---

## Flag

```
picoCTF{n0t_x0r_i5_r3v3r5ibl3_w17h_x0r_9cdb2757}
```

---

## What I Learned

- How XOR encryption works.
- XOR is its own inverse.
- If:

```
X ^ Y = Z
```

then

```
Z ^ Y = X
```

- Reading the source code often reveals exactly how to recover the password.
- Writing a small helper program is much faster than decoding values manually.

---

## Concepts Practiced

- Java source code analysis
- Reverse engineering
- XOR operation
- Byte arrays
- Writing helper programs for automation

---

## Key Takeaway

This challenge demonstrated one of the most important properties of XOR:

```
Encryption:
Plaintext ^ Key = Ciphertext

Decryption:
Ciphertext ^ Key = Plaintext
```

By understanding that XOR is reversible with the same key, I was able to recover the original password by writing a short Java program instead of decoding every byte manually. This reinforced the importance of understanding the underlying algorithm rather than trying to guess the password.