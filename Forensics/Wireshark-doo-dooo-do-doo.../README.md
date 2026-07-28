# picoCTF 2021 - Wireshark doo dooo do doo... Writeup

## Challenge Information

- **Challenge:** Wireshark doo dooo do doo...
- **Category:** Forensics
- **Difficulty:** Medium
- **Platform:** picoCTF 2021

## Description

This challenge provides a packet capture file:

```
shark1.pcapng
```

The objective is to analyze the network traffic and recover the hidden flag.

---

## Challenge I Faced

At first, I confirmed that the file was a packet capture and opened it using Wireshark.

While inspecting the packets, I noticed HTTP traffic. By following the HTTP stream, I found what looked like a flag, but it was still unreadable.

After examining the text more closely, I recognized that it was encoded using the **ROT13 (Caesar Shift 13)** cipher.

---

## My Approach

### 1. Verify the file type

I first identified the downloaded file.

```bash
file shark1.pcapng
```

Output:

```
shark1.pcapng: pcapng capture file - version 1.0
```

This confirmed that the file was a valid **PCAPNG network capture**.

---

### 2. Open the capture in Wireshark

I opened the capture using Wireshark.

```bash
wireshark shark1.pcapng
```

---

### 3. Inspect the HTTP traffic

While browsing the packets, I found an HTTP request and followed the HTTP stream.

The response contained:

```
Gur synt vf cvpbPGS{c33xno00_1_f33_h_qrnqorrs}
```

Although it resembled a picoCTF flag, it was still encrypted.

---

### 4. Recognize the cipher

The sentence:

```
Gur synt vf ...
```

is a well-known indicator of **ROT13** because it decodes to:

```
The flag is ...
```

Since ROT13 is simply a Caesar cipher with a shift of 13, I wrote a small Python script to decrypt it.

---

### 5. Decrypt the flag

```python
def decrypt(txt):
    result = ''

    for i in range(len(txt)):
        if txt[i] >= 'a' and txt[i] <= 'z':
            ch_pos = ord(txt[i]) - 97
            new_pos = (ch_pos - 13) % 26
            result += chr(new_pos + 97)
        else:
            result += txt[i]

    return result

print(decrypt("cvpbPGS{c33xno00_1_f33_h_qrnqorrs}"))
```

Running the script recovered the original flag.

---

## What I Learned

- `file` identifies packet capture formats such as **PCAPNG**.
- Wireshark is an essential tool for network forensic analysis.
- **Follow HTTP Stream** reconstructs the complete HTTP conversation, making it much easier to inspect transmitted data.
- Sometimes the flag is transmitted in plain text but encoded with a simple cipher.
- **ROT13** is a Caesar cipher with a fixed shift of **13**.
- Recognizing common encrypted phrases (such as `"Gur synt vf"` → `"The flag is"`) can quickly identify the encryption method.
- Writing a small Python script is an effective way to automate Caesar cipher decryption.

---

## Flag

```text
picoCTF{p33kab00_1_s33_u_deadbeef}
```