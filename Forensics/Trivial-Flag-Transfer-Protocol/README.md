# picoCTF 2021 - Trivial Flag Transfer Protocol Writeup

## Challenge Information

- **Challenge:** Trivial Flag Transfer Protocol
- **Category:** Forensics
- **Difficulty:** Medium
- **Platform:** picoCTF 2021

## Description

This challenge provides a network capture file:

```
tftp.pcapng
```

The objective is to analyze the captured TFTP traffic and recover the hidden flag.

The hint suggests that the flag may be hidden in a file transferred over the network.

---

## Challenge I Faced

At first, I inspected the packet capture using Wireshark.

After identifying that the traffic used the **Trivial File Transfer Protocol (TFTP)**, I exported all transferred files from the capture.

The exported files included several images and text files. Reading the text files provided instructions and a password, which hinted that the flag was hidden inside one of the images.

---

## My Approach

### 1. Open the packet capture

First, I opened the packet capture using Wireshark.

```bash
wireshark tftp.pcapng
```

---

### 2. Export the transferred files

Since the traffic used **TFTP**, I exported the transferred objects.

From the menu:

```
File
    └── Export Objects
            └── TFTP
```

The exported files included:

```
instructions.txt
plan
program.deb
picture1.bmp
picture2.bmp
picture3.bmp
```

---

### 3. Read the text files

The exported text files contained instructions explaining how to continue the challenge.

One of the files also revealed the password:

```
DUEDILIGENCE
```

The instructions indicated that the flag was hidden inside one of the BMP images.

---

### 4. Extract the hidden data

Since BMP files commonly support steganography, I used **steghide** to extract hidden data from the image.

```bash
steghide extract -sf picture3.bmp -p DUEDILIGENCE
```

Output:

```
wrote extracted data to "flag.txt".
```

---

### 5. Read the extracted file

Finally, I displayed the contents of the extracted file.

```bash
cat flag.txt
```

Output:

```
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
```

The flag was successfully recovered.

---

## What I Learned

- **TFTP (Trivial File Transfer Protocol)** is a simple protocol used to transfer files over UDP.
- Wireshark can reconstruct transferred files using:
  ```
  File → Export Objects → TFTP
  ```
- Packet captures may contain files that provide hints, passwords, or other information needed to solve the challenge.
- **Steghide** is commonly used to hide and extract data inside image and audio files.
- The basic syntax for extracting hidden data with Steghide is:

```bash
steghide extract -sf <file> -p <password>
```

where:

- `extract` extracts hidden data.
- `-sf` specifies the stego file.
- `-p` provides the passphrase.

- Many forensic challenges require combining multiple techniques. In this challenge:
  1. Analyze network traffic.
  2. Export transferred files.
  3. Read the provided instructions.
  4. Recover hidden data using steganography.

---

## Flag

```text
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
```