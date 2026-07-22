# Sleuthkit Intro – picoCTF 2022

## Challenge Information
- **Category:** Forensics
- **Difficulty:** Medium


## Challenge Description
The challenge provides a compressed disk image and asks us to use the Sleuth Kit tool `mmls` to find the size of the Linux partition. The correct partition size must be submitted to the remote checker to retrieve the flag.

---
## Flag
picoCTF{mm15_f7w!}

## My Approach


1. Checked the provided file type:

```bash
file disk.img.gz
disk.img.gz: gzip compressed data, was "disk.img"
file disk.img.gz
gunzip disk.img.gz
file disk.img
sudo apt install sleuthkit
mmls disk.img
nc saturn.picoctf.net 56299
