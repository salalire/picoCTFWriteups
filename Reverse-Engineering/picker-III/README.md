# Picker III

## Challenge Information
- **Category:** Reverse Engineering
- **Difficulty:** Medium

## Description
This challenge introduces a function table that restricts which functions can be executed. The objective is to analyze how the table is used and determine whether it can be modified to execute hidden functionality.

## Skills Learned
- Reading Python source code
- Understanding function tables
- Tracing program control flow
- Analyzing the use of `eval()` and `exec()`
- Identifying writable global variables

## Tools Used
- Python
- Linux Terminal
- Static code analysis

## Approach
1. Analyze how function calls are performed.
2. Trace the execution from `call_func()` to `get_func()`.
3. Identify the function table as the source of callable functions.
4. Inspect program features that allow modifying global variables.
5. Update the function table to redirect execution.

## What I Learned
This challenge taught me that restricting execution with a function table is only effective if the table itself is protected. I also learned to trace execution backwards from dangerous functions like `eval()` to identify controllable inputs.
## Flag
picoCTF{7h15_15_wh47_w3_g37_w17h_u53r5_1n_ch4rg3_226dd285}