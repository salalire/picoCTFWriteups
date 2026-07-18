# Magikarp Ground Mission

## Challenge

Connect to the remote machine using SSH, navigate through the Linux filesystem, and collect the three parts of the flag.

---

## My Approach

1. Connected to the remote machine using SSH.
2. Listed the files in the current directory.
3. Read the first part of the flag and the instructions.
4. Navigated through the filesystem to locate the remaining flag parts.
5. Combined all three parts to obtain the complete flag.

---

## Commands/Tools Used

```bash
ssh -p <PORT> ctf-player@<HOST>
pwd
ls
cd
cat
file
```

- SSH
- Linux Terminal

---

## What I Learned

- How to connect to a remote Linux machine using SSH.
- How to navigate the Linux filesystem using `cd`, `pwd`, and `ls`.
- The difference between the root directory (`/`) and the home directory (`~`).
- That changing directories does not remove or lose files—they remain in their original locations.

---

## Key Takeaway

Understanding the Linux filesystem hierarchy and confidently navigating between directories is an essential skill for CTF challenges and real-world Linux environments.
## Flag
picoCTF{xxsh_0ut_0f_//4t3r_0b24fc4f}