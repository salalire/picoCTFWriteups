# picoCTF 2024 - information Writeup

## Challenge Information

- **Challenge:** information
- **Category:** Forensics
- **Difficulty:** Easy
- **Platform:** picoCTF 2024

## Description

This challenge provides a JPEG image:

```
cat.jpg
```

The objective is to inspect the image and recover the hidden flag.

The challenge description hints that files can be modified in secret ways, suggesting that important information may be stored in the file's metadata.

---

## Challenge I Faced

Initially, I considered checking the image for hidden files, steganography, and embedded data.

Before trying more advanced forensic techniques, I decided to inspect the image metadata.

While examining the metadata, I found an unusual value stored in the **License** field that looked like a Base64-encoded string.

---

## My Approach

### 1. Inspect the image metadata

I examined the metadata using **ExifTool**.

```bash
exiftool cat2.jpg
```

Among the metadata fields, I found:

```
License:
cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
```

This value immediately stood out because it only contained Base64 characters.

---

### 2. Decode the Base64 string

I decoded the Base64 value.

```
cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
```

The decoded text was:

```
picoCTF{the_m3tadata_1s_modified}
```

This revealed the flag.

---

## What I Learned

- Image files contain metadata in addition to the visible image.
- Metadata can store information such as:
  - Author
  - Copyright
  - Camera information
  - GPS coordinates
  - License
  - Comments
- `exiftool` is one of the most useful forensic tools for viewing image metadata.
- Metadata fields may contain encoded or hidden information.
- Base64 is an encoding format, not encryption, and is commonly recognized by its character set (`A-Z`, `a-z`, `0-9`, `+`, `/`, `=`).
- Before attempting advanced forensic techniques such as steganography, it is often worth checking the metadata first.

---

## Flag

```text
picoCTF{the_m3tadata_1s_modified}
```