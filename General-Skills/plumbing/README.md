# plumbing

## Category
General Skills

## Difficulty
Medium

## What I Learned
- Used Linux pipes (`|`) to send the output of one command directly to another.
- Learned that not every program writes its output to a file; sometimes data must be processed as it is produced.
- Used `grep` to filter program output and extract the flag.

## Approach
1. Connected to the remote service using `nc`.
2. Piped the program's output into `grep`.
3. Searched for the `picoCTF{}` flag format and recovered the flag.

## Commands Used

## Flag
picoCTF{digital_plumb3r_A01Bc3eC}


```bash
nc <host> <port> | grep "picoCTF{"