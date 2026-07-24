# picoCTF 2019 - extensions Writeup

## Challenge Information

- **Challenge:** extensions
- **Category:** Forensics
- **Difficulty:** Medium
- **Platform:** picoCTF 2019

## Description

his is a really weird text file. Can you find the flag?

Get the flag from TXT
.

---

## Challenge I Faced

Initially, the file appeared to be an ordinary text file because of its `.txt` extension.

The main challenge was recognizing that the extension was intentionally misleading and that I needed to determine the actual file type before attempting further analysis.

---

## My Approach

### 1. Identify the real file type

I first checked the file using the `file` command.

```bash
file flag.txt
```

Output:

```
flag.txt: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced
```

This immediately revealed that the file was actually a **PNG image**, despite having a `.txt` extension.

---

### 2. Search for printable strings

I searched for the flag using `strings`.

```bash
strings flag.txt | grep pico
```

No results were found.

---

### 3. Inspect the file structure

I used `binwalk` to identify embedded data.

```bash
binwalk flag.txt
```

Output:

```
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image
91            0x5B            Zlib compressed data
```

This confirmed that the file was a valid PNG image.

---

### 4. View image metadata

Next, I inspected the metadata.

```bash
exiftool flag.txt
```

The output confirmed the image properties but did not reveal the flag.

---

### 5. Open the image

Since the file was identified as a PNG image, I opened it using GIMP.

```bash
gimp flag.txt
```

The image displayed the hidden flag directly.

---

## What I Learned

- File extensions can be intentionally misleading.
- The `file` command determines a file's actual type by inspecting its signature (magic bytes), not its filename.
- `strings` is useful for extracting printable text, but it does not always reveal hidden information.
- `binwalk` helps identify embedded or compressed data inside binary files.
- `exiftool` is useful for examining image metadata.
- When analyzing forensic challenges, always verify the actual file type before relying on the file extension.
- Image editors such as GIMP can be useful for viewing files that are disguised with incorrect extensions.

---

## Flag

```text
picoCTF{now_you_know_about_extensions}
```