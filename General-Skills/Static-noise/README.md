# Static ain't always noise

## Challenge
Analyze the provided binary and locate the hidden flag without modifying or exploiting the program.

## What I Learned
- How to inspect an ELF binary using the `file` command.
- How to extract printable strings from a binary using `strings`.
- How to filter output with `grep` to quickly locate useful information.
- The difference between static analysis (examining the binary without running it) and dynamic analysis (using tools like GDB).

## Tools Used
- `file`
- `strings`
- `grep`

## Commands Used

```bash
file static
strings static
strings static | grep pico
```

## Challenge
At first I explored the binary with GDB, but I realized the flag was stored as plain text inside the executable. Static analysis with `strings` was the fastest and simplest solution.

## Result
Successfully extracted the flag from the binary using static analysis.
## Flag
picoCTF{d15a5m_t34s3r_20335e41}
