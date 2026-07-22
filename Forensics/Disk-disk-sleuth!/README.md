# picoCTF 2021 - Disk, disk, sleuth! Writeup

## Challenge Information

- **Challenge:** Disk, disk, sleuth!
- **Category:** Forensics
- **Difficulty:** Medium
- **Platform:** picoCTF 2021

## Description

This challenge provides a compressed disk image file:

```
dds1-alpine.flag.img.gz
```

The goal is to analyze the disk image and find the hidden flag using forensic techniques.

The challenge hint suggests using:

- `srch_strings` from The Sleuth Kit
- Terminal tools for searching inside the disk image

---

## Challenge I Faced

At first, the disk image looked like a normal binary file, and using regular commands such as `cat` would not provide useful information.

The main challenge was understanding that a disk image is not just a normal file. It contains partitions, filesystems, and possibly hidden data.

---

## My Approach

### 1. Identify the file type

First, I checked the compressed file:

```bash
file dds1-alpine.flag.img.gz
```

Output:

```
gzip compressed data
```

This showed that the file was compressed, so I extracted it.

---

### 2. Extract the disk image

I decompressed the file using:

```bash
gunzip dds1-alpine.flag.img.gz
```

This produced:

```
dds1-alpine.flag.img
```

---

### 3. Analyze the disk image

I checked the image format:

```bash
file dds1-alpine.flag.img
```

Output:

```
DOS/MBR boot sector
partition 1: ID=0x83
```

This showed that the file was a Linux disk image containing a partition.

---

### 4. Search for the flag

Instead of manually mounting the image, I used the `strings` command to extract readable text from the disk image and searched for the picoCTF flag format:

```bash
strings dds1-alpine.flag.img | grep pico
```

The flag was found:

```
SAY picoCTF{f0r3ns1c4t0r_n30phyt3_5e56e786}
```

---

## What I Learned

- Disk images contain complete filesystems, not just normal text data.
- The `file` command can reveal important information about unknown files.
- Compressed forensic files should be extracted before analysis.
- `strings` is useful for finding hidden readable data inside binary files.
- In CTF forensics, simple command-line tools can sometimes solve problems quickly before using advanced tools.

---

## Flag

```
picoCTF{f0r3ns1c4t0r_n30phyt3_5e56e786}
```