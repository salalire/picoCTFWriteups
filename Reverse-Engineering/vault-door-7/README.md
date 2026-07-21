# picoCTF 2019 - Vault Door 7 Writeup

## Challenge Information

- **Challenge:** Vault Door 7
- **Category:** Reverse Engineering
- **Difficulty:** Hard

## Description

This challenge uses bit shifts to convert a password string into an array of integers.

The program takes a 32-character password and packs every 4 characters into a single integer using bit manipulation.

The important part of the source code is:

```java
x[i] = hexBytes[i*4]   << 24
     | hexBytes[i*4+1] << 16
     | hexBytes[i*4+2] << 8
     | hexBytes[i*4+3];
```

This means the program combines four ASCII characters into one 32-bit integer.

For example:

```
Characters:

A  _  b  1

ASCII values:

0x41 0x5F 0x62 0x31

Packed integer:

0x415F6231
```

The password characters are converted into integers, so the goal is to reverse this process and recover the original characters.

---

## Challenge I Faced

At first, I tried to manually convert the decimal integer values into hexadecimal and then use an ASCII table to find the characters.

This approach works, but it is slow and not the best way to solve reverse engineering challenges.

The main challenge was understanding that the integers were not random values. They were actually containing four hidden ASCII characters packed together.

---

## My Approach

The original program uses left shifts (`<<`) to pack four bytes into one integer.

Example:

```
byte1 << 24
byte2 << 16
byte3 << 8
byte4
```

To reverse it, I used the opposite operation:

```
>>> 24  -> extract first byte
>>> 16  -> extract second byte
>>> 8   -> extract third byte
no shift -> extract fourth byte
```

I also used:

```java
& 0xFF
```

to keep only the lowest 8 bits because each character is represented by one byte.

The final decoder:

```java
public class Decode {

    public static void main(String[] args) {

        int[] nums = {
            1096770097,
            1952395366,
            1600270708,
            1601398833,
            1716808014,
            1734305378,
            825374004,
            912340068
        };

        StringBuilder password = new StringBuilder();

        for (int n : nums) {
            password.append((char)((n >>> 24) & 0xFF));
            password.append((char)((n >>> 16) & 0xFF));
            password.append((char)((n >>> 8) & 0xFF));
            password.append((char)(n & 0xFF));
        }

        System.out.println(password);
    }
}
```

---

## What I Learned

- A 32-bit integer can store four separate bytes.
- Bit shifting can be used to pack and unpack data.
- The reverse of left shifting (`<<`) is extracting data using right shifting (`>>>`).
- The `& 0xFF` mask is used to extract a single byte.
- In reverse engineering, data that looks like random numbers may actually contain encoded information.

This challenge improved my understanding of low-level data representation and byte manipulation.

---

## Flag

```
picoCTF{A_b1t_0f_b1t_sh1fTiNg_39e852dd82}
```