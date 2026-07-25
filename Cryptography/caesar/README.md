# picoCTF 2019 - The Numbers Writeup

## Challenge Information

- **Challenge:** The Numbers
- **Category:** Cryptography
- **Difficulty:** Medium
- **Platform:** picoCTF 2019

## Description

This challenge provides an encrypted message:

```
apmqqglerfcpszgamlexqtsfyd
```

The objective is to decrypt the ciphertext and recover the hidden flag.

---

## Challenge I Faced

The challenge did not explicitly know the shift key for the challenge
I first analyzed the ciphertext and noticed that it only contained lowercase alphabetic characters, suggesting that it might be a classical substitution cipher.

By testing different Caesar cipher shifts, I found that shifting each character **24 positions backward** (equivalent to shifting **2 positions forward**) successfully decrypted the message.

---

## My Approach

I wrote a simple Python script to reverse the Caesar cipher.

```python
def decrypt(txt):
    result = ''

    for i in range(len(txt)):
        ch_pos = ord(txt[i])
        ch_pos = ch_pos - 97

        new_pos = ch_pos - 24
        new_pos = new_pos % 26

        new_ch = chr(new_pos + 97)

        result += new_ch

    return result


print(decrypt("apmqqglerfcpszgamlexqtsfyd"))
```

The script works by:

1. Converting each character into its alphabet index (`a = 0`, `b = 1`, ...).
2. Applying a Caesar shift of **24** positions.
3. Using modulo (`% 26`) to wrap around the alphabet.
4. Converting the result back into characters.
5. Building the decrypted message.

Running the script produces the original plaintext.

---

## What I Learned

- A Caesar cipher shifts every letter by a fixed number of positions.
- `ord()` converts a character to its ASCII value.
- `chr()` converts an ASCII value back to a character.
- Converting characters to alphabet indices (`0-25`) simplifies Caesar cipher operations.
- The modulo operator (`% 26`) wraps the alphabet when shifting past `z` or before `a`.
- When the shift value is unknown, trying all 26 possible shifts (brute force) is often an effective approach for Caesar ciphers.

---

## Flag

```text
picoCTF{crossingtherubiconvfhsjkou}
```