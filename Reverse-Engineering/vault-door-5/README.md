# Vault Door 5

**Category:** Reverse Engineering  
**Difficulty:** Medium  


---

## Description

The goal of this challenge is to recover the vault password by analyzing the Java source code.




---

## Source Code Analysis

The important part of the program is:

```java
String urlEncoded = urlEncode(password.getBytes());
String base64Encoded = base64Encode(urlEncoded.getBytes());

return base64Encoded.equals(expected);
```

The password is processed in two steps:

1. URL Encoding
2. Base64 Encoding

The program compares the final encoded string with the hardcoded `expected` value.

Since the program **encodes** the password before checking it, we simply need to perform the opposite operations.

---

## My Thought Process

I first read the Java source code to understand how the password was being processed.

After reading the `checkPassword()` method, I noticed that the password is:

```
Password
    ↓
URL Encode
    ↓
Base64 Encode
    ↓
Compare with expected
```

That means the solution is simply to reverse the process.

Using the challenge hint, I decoded the expected string by performing the reverse operations:

```
Base64 Decode
        ↓
URL Decode
        ↓
Original Password
```

After reversing both encodings, I obtained the correct password and submitted it in the required format.

---

## Solution

Transformation used by the program:

```
Password
    ↓
URL Encode
    ↓
Base64 Encode
```

Reverse transformation:

```
Expected String
        ↓
Base64 Decode
        ↓
URL Decode
        ↓
Password
```

Submit as:

```
picoCTF{c0nv3rt1ng_fr0m_ba5e_64_42c6409b}
```

---

## Flag

```
picoCTF{c0nv3rt1ng_fr0m_ba5e_64_42c6409b}
```

---

## What I Learned

- Read the source code before trying random tools.
- Base64 is an encoding method, not encryption.
- URL encoding converts characters into `%xx` hexadecimal format.
- To recover the original data, reverse the operations in the opposite order.
- Source code often tells  exactly how to solve a reverse engineering challenge.

---

## Concepts Practiced

- Java source code analysis
- Reverse engineering
- Base64 encoding and decoding
- URL encoding and decoding
- Understanding encoding pipelines

---

## Key Takeaway

This challenge reinforced an important reverse engineering principle:

**If a program transforms data before comparing it, recover the original value by reversing those transformations in the opposite order.**

Instead of guessing the password, reading the source code revealed exactly how it was constructed, making the solution straightforward.