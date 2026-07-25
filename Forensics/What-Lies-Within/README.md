# picoCTF 2019 - What Lies Within Writeup

## Challenge Information

- **Challenge:** What Lies Within
- **Category:** Forensics
- **Difficulty:** Medium
- **Platform:** picoCTF 2019

## Description

There's something in the building
. Can you retrieve the flag?
---

## Challenge I Faced

Initially, the image looked completely normal. I first checked for embedded strings, metadata, and hidden files, but none of these revealed the flag.

The challenge was recognizing that the image likely contained **hidden pixel data** rather than visible content or metadata.

---

## My Approach

### 1. Verify the file type

I first identified the file.

```bash
file buildings.png
```

Output:

```
PNG image data, 657 x 438, 8-bit/color RGBA, non-interlaced
```

This confirmed that the file was a valid PNG image.

---

### 2. Search for printable strings

I searched for the flag using the `strings` command.

```bash
strings buildings.png | grep pico
```

No results were returned.

---

### 3. Inspect the metadata

Next, I examined the image metadata.

```bash
exiftool buildings.png
```

The metadata only contained normal image information and did not reveal the flag.

---

### 4. Check for embedded files

I inspected the image using `binwalk`.

```bash
binwalk buildings.png
```

Output:

```
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image
41            0x29            Zlib compressed data
```

The image appeared to be a normal PNG without any obvious embedded files.

---

### 5. Analyze the image for steganography

Since the previous techniques did not reveal the flag, I used **zsteg** to search for hidden information stored in the image pixels.

```bash
zsteg buildings.png
```

Output:

```
b1,rgb,lsb,xy .. text:
picoCTF{h1d1ng_1n_th3_b1t5}
```

The flag was hidden inside the **Least Significant Bits (LSB)** of the RGB channels.

---

## What I Learned

- `file` verifies the real file type regardless of its extension.
- `strings` only extracts printable text and cannot detect most steganography.
- `exiftool` is useful for inspecting image metadata.
- `binwalk` helps identify embedded files or compressed data inside binary files.
- Hidden information may be stored directly inside an image's pixel data rather than in metadata or appended files.
- **LSB (Least Significant Bit) steganography** hides data by modifying the least significant bits of image pixels with minimal visual changes.
- `zsteg` is one of the most useful tools for detecting LSB steganography in PNG and BMP images.

---

## Flag

```text
picoCTF{h1d1ng_1n_th3_b1t5}
```