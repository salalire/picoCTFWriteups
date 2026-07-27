# picoCTF 2024 - C3 Writeup

## Challenge Information

- **Challenge:** C3
- **Category:** Cryptography
- **Difficulty:** Easy
- **Platform:** picoCTF 2024

## Description

This challenge provides an encrypted file:

```
enc_flag
```

The objective is to recover the original flag hidden inside the file.

---

## Challenge I Faced

At first, I examined the file to determine what type of data it contained.

The output looked like Base64 because it only contained Base64 characters (`A-Z`, `a-z`, `0-9`, `+`, `/`, `=`). However, decoding it only once did not immediately reveal the flag.

After decoding multiple times, I eventually obtained another string that resembled a flag but was still unreadable.

I recognized that it was encrypted with a **Caesar cipher**, so I wrote a Python script to reverse the shift.

---

## My Approach

### 1. Inspect the file

First, I extracted the printable contents of the file.

```bash
strings enc_flag
```

Output:

```
YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclh6ZzJhMnd6TW1zeWZRPT0nCg==
```

---

### 2. Decode the Base64 data

I wrote a simple Python script to decode the Base64 string.

```python
import base64

def decode_base64(encoded_str):
    decoded_bytes = base64.b64decode(encoded_str)
    return decoded_bytes.decode("utf-8")

print(decode_base64("YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclh6ZzJhMnd6TW1zeWZRPT0nCg=="))
```

After decoding multiple Base64 layers, I obtained:

```
wpjvJAM{jhlzhy_k3jy9wa3k_86kl32k2}
```

Although it resembled a picoCTF flag, it was still encrypted.

---

### 3. Reverse the Caesar cipher

I noticed that the letters appeared to be shifted.

I wrote the following Python script to decrypt the text using a Caesar shift of **7**.

```python
def decrypt(txt):
    result = ''

    for ch in txt:
        if 'a' <= ch <= 'z':
            pos = ord(ch) - ord('a')
            pos = (pos - 7) % 26
            result += chr(pos + ord('a'))
        else:
            result += ch

    return result

print(decrypt("wpjvJAM{jhlzhy_k3jy9wa3k_86kl32k2}"))
```

Running the script recovered the original flag.

---

## What I Learned

- `strings` extracts printable data from binary files.
- Base64 is an encoding scheme, **not encryption**.
- Some CTF challenges use multiple layers of encoding.
- A decoded result is not always the final answer; it may still be encrypted.
- Caesar cipher shifts each alphabetic character by a fixed number of positions.
- `ord()` and `chr()` make implementing Caesar cipher decryption straightforward.
- When analyzing cryptography challenges, solve each encoding or encryption layer one at a time.

---

## Flag

```text
picoCTF{caesar_d3cr9pt3d_86de32d2}
```