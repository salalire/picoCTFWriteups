# picoCTF 2022 - Sleuthkit Apprentice Writeup

## Challenge Information

- **Challenge:** Sleuthkit Apprentice
- **Category:** Forensics
- **Difficulty:** Medium
- **Platform:** picoCTF 2022

## Description

Download this disk image and find the flag.

Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

---

## Challenge I Faced

Unlike the previous challenges, this disk image contains multiple partitions instead of a single Linux partition.

The main challenge was determining which partition contained the filesystem with the flag before attempting to recover it.

---

## My Approach

### 1. Identify the disk image

First, I checked the file type.

```bash
file disk.flag.img
```

Output:

```
DOS/MBR boot sector
Partition 1 : Linux
Partition 2 : Linux Swap
Partition 3 : Linux
```

This indicated that the disk image contains three partitions.

---

### 2. View the partition table

To determine the starting sector of each partition, I used:

```bash
mmls disk.flag.img
```

Output:

```
Partition 1 : Start Sector = 2048
Partition 2 : Start Sector = 206848
Partition 3 : Start Sector = 360448
```

These starting sectors are required as offsets for Sleuth Kit tools.

---

### 3. Inspect each partition

I first examined the first partition:

```bash
fls -r -o 2048 disk.flag.img | grep flag
```

No results were found.

Next, I checked the swap partition:

```bash
fls -r -o 206848 disk.flag.img | grep flag
```

Output:

```
Cannot determine file system type
```


Finally, I searched the third partition:

```bash
fls -r -o 360448 disk.flag.img | grep flag
```

Output:

```
++ r/r * 2082(realloc): flag.txt
++ r/r 2371: flag.uni.txt
```

The third partition contained the flag files.

---

### 4. Recover the flag

I extracted the Unicode flag file using its inode.

```bash
icat -o 360448 disk.flag.img 2371
```

Output:

```
picoCTF{by73_5urf3r_3497ae6b}
```

---

## What I Learned

- A disk image may contain multiple partitions.
- `file` quickly identifies the type of a disk image.
- `mmls` displays the partition table and starting sector of each partition.
- Each filesystem must be accessed using its correct offset.
- Swap partitions do not contain standard filesystems.
- `fls` lists files within a filesystem.
- `grep` can quickly locate target filenames.
- `icat` extracts the contents of a file directly from its inode.
- In forensic investigations, identifying the correct partition is an important first step before analyzing files.

---

## Flag

```text
picoCTF{by73_5urf3r_3497ae6b}
```