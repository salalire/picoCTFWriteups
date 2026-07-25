# picoCTF 2022 - St3g0 Writeup

## Challenge Information

- **Challenge:** St3g0
- **Category:** Forensics
- **Difficulty:** Medium
- **Platform:** picoCTF 2022

## Description

ownload this image and find the flag.

Download image

---

## Challenge I Faced

At first, I treated the file like a normal image and checked its metadata and embedded strings.

Although the file appeared to be a valid PNG image, none of the common forensic tools revealed the flag.

The challenge was recognizing that the flag was hidden using **LSB (Least Significant Bit) steganography**, requiring a specialized steganography tool.

---

## My Approach

### 1. Verify the file type

First, I identified the file.

```bash
file pico.flag.png
```

Output:

```
PNG image data, 585 x 172, 8-bit/color RGBA, non-interlaced
```

The file was confirmed to be a valid PNG image.

---

### 2. Search for printable strings

I searched for the flag using the `strings` command.

```bash
strings pico.flag.png | grep pico
```

No results were returned.

---

### 3. Inspect the metadata

I examined the image metadata.

```bash
exiftool pico.flag.png
```

The metadata only contained normal image information and did not reveal the flag.

---

### 4. Inspect the image structure

I checked whether additional files or compressed data were embedded inside the PNG.

```bash
binwalk pico.flag.png
```

Output:

```
PNG image
Zlib compressed data
```

This confirmed that the image was a normal PNG file and did not immediately expose the flag.

---

### 5. Analyze for steganography

Since the previous techniques did not reveal anything, I analyzed the image using **zsteg**, a tool designed to detect hidden data in PNG and BMP images.

```bash
zsteg pico.flag.png
```

Output:

```
b1,rgb,lsb,xy .. text:
picoCTF{7h3r3_15_n0_5p00n_a1062667}$t3g0
```

The flag was successfully recovered from the **Least Significant Bits (LSB)** of the image.

---

## What I Learned

- `file` verifies the actual file type.
- `strings` only extracts printable text and cannot detect most steganography.
- `exiftool` is useful for inspecting image metadata.
- `binwalk` identifies embedded files and compressed data inside binaries.
- Hidden data is not always stored in metadata or appended to the file.
- **LSB (Least Significant Bit) steganography** hides information by modifying the least significant bits of image pixels.
- `zsteg` is an effective tool for detecting hidden data inside PNG and BMP images.

---

## Flag

```text
picoCTF{7h3r3_15_n0_5p00n_a1062667}
```