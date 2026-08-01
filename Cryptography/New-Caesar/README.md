# picoCTF 2021 - New Caesar Writeup

## Challenge Information

- **Challenge:** New Caesar
- **Category:** Cryptography
- **Difficulty:** Medium
- **Platform:** picoCTF 2021

---

## Description

This challenge introduces a modified version of the Caesar cipher.

Instead of using the normal alphabet of 26 letters, the cipher only uses the first **16 lowercase letters**:

```python
ALPHABET = "abcdefghijklmnop"
```

The encrypted message is:

```text
fegdeogdgecoeocgcgchcfcffccfca
```

The goal is to recover the original plaintext and submit it as:

```text
picoCTF{...}
```

---

## Challenge I Faced

At first, this looked like an ordinary Caesar cipher.

However, after examining the provided source code (`new_caesar.py`), I noticed several important differences:

- The alphabet contains only **16 letters** instead of 26.
- Every character represents **4 bits (a nibble)** instead of an entire byte.
- Two encrypted letters together represent one ASCII character.
- The encryption key is unknown, so every possible key must be tested.

Instead of trying to reverse the encryption manually, I wrote a Python script to brute-force every possible key.

---

# My Approach

## Step 1. Understand the custom alphabet

The source code defines:

```python
ALPHABET = string.ascii_lowercase[:16]
```

which produces:

```text
abcdefghijklmnop
```

Each character therefore represents a value between:

```text
a = 0000
b = 0001
c = 0010
...
p = 1111
```

Unlike normal Caesar cipher, each encrypted character represents only **4 bits**.

---

## Step 2. Recover the shifted text

Since the encryption is still a Caesar shift, I tried every possible key.

There are only 16 possible keys:

```python
for key in ALPHABET:
```

For every key, I shifted every ciphertext character backwards.

```python
shifted += ALPHABET[
    (ALPHABET.index(c) - ALPHABET.index(key)) % 16
]
```

This reverses the Caesar shift.

---

## Step 3. Convert every two letters back into one byte

After removing the Caesar shift, the text still was not readable.

The reason is that each character represents only four bits.

For every pair of characters:

```python
for i in range(0, len(shifted), 2):
```

I converted each letter into its binary representation.

```python
b = format(ALPHABET.index(shifted[i]), "04b")
```

Example:

```
c -> 0010
```

Then I converted the second character:

```python
b += format(ALPHABET.index(shifted[i + 1]), "04b")
```

Example:

```
0010
+
0101
=
00100101
```

Now I had one complete byte.

---

## Step 4. Convert the byte into an ASCII character

Once the eight-bit binary string was complete, I converted it into a character.

```python
flag += chr(int(b, 2))
```

Example:

```
00100101
↓

37

↓

'%'
```

Repeating this for every pair reconstructed the plaintext.

---

## Step 5. Try every possible key

Finally, I printed every candidate plaintext.

```python
print(key, ":", flag)
```

One of the outputs clearly contained the flag.

---

# Python Solution

```python
import string

ALPHABET = string.ascii_lowercase[:16]
cipher = "fegdeogdgecoeocgcgchcfcffccfca"

for key in ALPHABET:

    shifted = ""

    for c in cipher:
        shifted += ALPHABET[
            (ALPHABET.index(c) - ALPHABET.index(key)) % 16
        ]

    flag = ""

    for i in range(0, len(shifted), 2):
        b = format(ALPHABET.index(shifted[i]), "04b")
        b += format(ALPHABET.index(shifted[i + 1]), "04b")
        flag += chr(int(b, 2))

    print(key, ":", flag)
```

---

# Why This Works

The encryption consists of **two separate steps**:

### Step 1

Apply a Caesar shift using a 16-character alphabet.

```
Plain nibble
      │
      ▼
Caesar Shift
      │
      ▼
Encrypted nibble
```

---

### Step 2

Each encrypted character stores only four bits.

```
Encrypted letter 1
        │
        ▼
First 4 bits

Encrypted letter 2
        │
        ▼
Last 4 bits

↓

8-bit ASCII

↓

Character
```

To decrypt, the process is simply reversed:

```
Ciphertext

↓

Undo Caesar Shift

↓

Recover 4-bit values

↓

Combine two nibbles

↓

ASCII character

↓

Plaintext
```

---

# What I Learned

- Caesar ciphers are not limited to 26-character alphabets.
- A custom alphabet changes the modulus used during shifting.
- Four bits are called a **nibble**.
- Two nibbles combine to form one byte.
- Binary data can be reconstructed from characters by converting each symbol into its numeric value.
- When the key space is very small (16 possibilities), brute force is often the simplest and most effective approach.
- Reading and understanding the provided source code is often the fastest way to solve reverse engineering and cryptography challenges.

---

# Key Concepts

- Custom Caesar Cipher
- Modular Arithmetic
- Brute Force
- Binary Representation
- Nibbles (4 bits)
- Bytes (8 bits)
- ASCII Encoding
- Python String Manipulation
- Cryptanalysis

---

