# Picker II

## Challenge Information
- **Category:** Reverse Engineering
- **Difficulty:** Medium

## Description
The program accepts user input and executes it using Python's `eval()` function. A filter prevents direct access to a specific function by blocking a keyword. The goal is to understand how the filter works and find another way to execute the hidden functionality.

## Skills Learned
- Reading and understanding Python source code
- Analyzing the behavior of `eval()`
- Understanding how input filters work
- Exploring Python's object model and function references
- Thinking beyond literal string matching

## Tools Used
- Python
- Linux Terminal
- Nano
- Static code analysis

## Approach
1. Read the Python source code.
2. Identify the program flow.
3. Analyze the input filter.
4. Understand what `eval()` actually executes.
5. Determine how the protected function could be reached without violating the filter.

## What I Learned
This challenge taught me that filtering user input is not always enough to secure programs. Understanding how Python resolves objects and evaluates expressions is essential when analyzing Python applications.

## Files
- Source code
- Screenshots
## Flag
picoCTF{f1l73r5_f41l_c0d3_r3f4c70r_m1gh7_5ucc33d_0b5f1131}