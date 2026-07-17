# Picker IV

## Challenge

The program reads a hexadecimal address from the user and jumps directly to that address using a function pointer. The objective is to redirect execution to the hidden `win()` function to print the flag.

---

## My Approach

1. Examined the provided C source code.
2. Identified the hidden `win()` function that prints the flag.
3. Opened the binary in GDB.
4. Used `info functions` to locate the address of `win()`.
5. Connected to the remote service using `nc`.
6. Entered the address of `win()` (without the `0x` prefix), causing the program to execute the hidden function and reveal the flag.

---

## Commands Used

```bash
file picker-IV
strings picker-IV.c
gdb picker-IV
```

Inside GDB:

```gdb
info functions
disassemble win
```

Run the remote service:

```bash
nc saturn.picoctf.net <PORT>
```

Input:

```
40129e
```

---

## What I Learned

- How function pointers work in C.
- How to locate function addresses using GDB.
- Why allowing user-controlled function pointers is a serious security vulnerability.
- The importance of analyzing source code before debugging a binary.

---

## Tools Used

- GDB
- Netcat
- file
- strings

---

## Key Takeaway

Never allow users to control function pointers or execution addresses. Doing so allows attackers to redirect program execution and potentially execute privileged functionality.
## Flag
picoCTF{n3v3r_jump_t0_u53r_5uppl13d_4ddr35535_b8de1af4}
