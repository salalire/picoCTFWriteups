# ASCII FTW

## Challenge
The binary constructs the flag using hexadecimal ASCII values stored in memory.

## What I Learned
- How ASCII characters are represented in hexadecimal.
- How to read assembly instructions that initialize memory.
- How to examine memory in GDB using different formats.
- The difference between viewing memory as hexadecimal (`x/x`) and as characters (`x/s`).

## Tools Used
- GDB
- Linux Terminal

## Key Commands

```bash
disassemble main
break *main+140
run
x/s $rbp-0x30
```

## Challenges Faced
- Initially converted every hexadecimal value manually.
- Later learned that GDB can display the entire string directly from memory.

## Takeaway
Understanding memory layouts and GDB's memory examination commands can save a huge amount of time during reverse engineering.
## Flag
picoCTF{ASCII_IS_EASY_3CF4BFAD}