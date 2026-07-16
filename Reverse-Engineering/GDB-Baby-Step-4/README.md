# GDB Baby Step 4

## Category

Reverse Engineering

## Difficulty

Easy

---

## Challenge Description

The challenge required determining the constant used inside a function that multiplies the value stored in the `EAX` register. The final flag is the multiplier represented in decimal.

---

## Skills Practiced

- Static Analysis
- Dynamic Analysis
- GDB
- Assembly Reading
- x86-64 Calling Convention
- Register Inspection

---

## Tools Used

- GDB
- Ghidra
- Linux Terminal

---

## Initial Thoughts

At first, I assumed that after the `call` instruction executed, the result would immediately appear in the `EAX` register.

While debugging, I realized that the `call` instruction only transfers execution to another function. The multiplication does not happen until the instructions inside the called function execute.

This helped me understand how function calls actually work at the assembly level.

---

## Static Analysis

Using Ghidra, I inspected the `func1()` function and identified the multiplication instruction.

```assembly
imul   $0x3269,%eax,%eax
```

From this instruction, it became clear that the constant multiplier was `0x3269`.

---

## Dynamic Analysis

Using GDB, I:

- Set a breakpoint before the function call.
- Entered the function using `si`.
- Observed the value of the `EAX` register before multiplication.
- Executed the multiplication instruction.
- Compared the register values before and after execution.

By dividing the final value by the initial value, I confirmed the multiplier dynamically.

---

## Challenges I Encountered

Initially, I believed that the `jump` command would execute an instruction.

After experimenting, I learned that:

- `jump` only changes the Instruction Pointer (`RIP`).
- It does **not** execute the instruction.
- The instruction still requires `si` or `ni` to run.

This clarified the difference between changing execution flow and actually executing instructions.

---

## Key Concepts Learned

- Function calls using `call`
- Function returns using `ret`
- Purpose of the `EAX` and `EDI` registers
- Difference between `jump` and `call`
- Difference between static and dynamic analysis
- Using breakpoints effectively
- Reading assembly instructions
- Understanding instruction execution order

---

## Useful GDB Commands

```bash
disassemble main
disassemble func1

break *main+38

run

si

ni

info registers

x/i $rip

finish
```

---

## Lessons Learned

This challenge taught me that understanding CPU execution flow is more important than memorizing GDB commands.

Instead of stepping through instructions randomly, I learned to:

- Identify the interesting instruction.
- Place breakpoints strategically.
- Observe register changes.
- Verify assumptions using dynamic analysis.

---

## Flag

```
picoCTF{1205}
```