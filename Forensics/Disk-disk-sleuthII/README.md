# picoCTF 2021 - Disk, disk, sleuth! II Writeup

## Challenge Information

- **Challenge:** Disk, disk, sleuth! II
- **Category:** Forensics
- **Difficulty:** Medium
- **Platform:** picoCTF 2021

## Description

This challenge provides a Linux disk image and tells us that the flag is stored in a file named:

```
down-at-the-bottom.txt
```

The objective is to locate the file inside the disk image and recover its contents.

---

## Challenge I Faced


The main challenge was understanding how to inspect a disk image, locate the correct partition, recursively search the filesystem, and extract a file using its inode.

---

## My Approach

### 1. Inspect the partition table

First, I identified the partition layout of the disk image.

```bash
mmls dds2-alpine.flag.img
```

Output:

```
DOS Partition Table

Linux Partition
Start Sector: 2048
```

This tells us that the filesystem begins at sector **2048**, which must be supplied to Sleuth Kit tools using the `-o` (offset) option.

---

### 2. List the filesystem

Running `fls` without an offset failed:

```bash
fls dds2-alpine.flag.img
```

Output:

```
Cannot determine file system type
```

After providing the correct offset:

```bash
fls -o 2048 dds2-alpine.flag.img
```

I was able to view the root directory of the filesystem.

---

### 3. Search for the target file

Since the challenge already gave the filename, I performed a recursive search.

```bash
fls -r -o 2048 dds2-alpine.flag.img | grep "down-at-the-bottom.txt"
```

Output:

```
+ r/r 18291: down-at-the-bottom.txt
```

This revealed that the file's inode number is **18291**.

---

### 4. Recover the file

Using the inode number, I extracted the file with `icat`.

```bash
icat -o 2048 dds2-alpine.flag.img 18291
```

The command displayed the contents of the file, including the flag.

---

## What I Learned

- `mmls` displays the partition table of a disk image.
- `fls` lists files and directories inside a filesystem.
- The `-o` option specifies the filesystem offset (starting sector).
- The `-r` option recursively searches through directories.
- Every file has an inode, which can be used to recover its contents.
- `icat` extracts a file directly from a disk image using its inode number.
- The Sleuth Kit provides powerful forensic tools for analyzing disk images without mounting them.

---

## Flag

```text
picoCTF{f0r3ns1c4t0r_n0v1c3_4bd721f2}
```