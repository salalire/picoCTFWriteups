# Glory of the Garden – picoCTF

## Challenge Information
- **Category:** Forensics
- **Difficulty:** Easy


## Challenge Description
This file contains more than it seems.

The challenge provides a file named `garden.jpg` and asks us to recover the hidden flag.

---

## Challenge

The goal was to inspect the JPEG image and determine whether any hidden data was embedded inside it.

---

## My Approach

1. Downloaded the provided image.
2. Verified the file type using:

```bash
file garden.jpg
```

3. Since the challenge hinted that the image contained more than it appeared, I extracted printable strings from the image:

```bash
strings garden.jpg
```

4. Scrolled through the output until I found a string matching the picoCTF flag format.

---

## What I Learned

- JPEG files can contain hidden metadata or embedded text.
- The `strings` command is a simple but powerful forensic tool for extracting printable text from binary files.
- Always inspect files before using more advanced forensic tools—the simplest method is often enough.

---

## Commands Used

```bash
file garden.jpg
strings garden.jpg
```

---

## Flag

```text
picoCTF{more_than_m33ts_the_3y3eBdBd2cc}
```