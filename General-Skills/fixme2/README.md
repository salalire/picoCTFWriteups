# Fixme2

## Description
This challenge provides a Python script containing a syntax error. The goal is to identify and fix the error so the script can execute and reveal the flag.

## Approach
- Checked the file type using `file`.
- Opened the script with `nano`.
- Ran the script using `python3` to identify the error location.
- Python reported a `SyntaxError` caused by using the assignment operator (`=`) inside an `if` statement.
- Replaced `=` with the comparison operator `==`.
- Saved the file and executed the script again to print the flag.
## Flag
picoCTF{3qu4l1ty_n0t_4551gnm3nt_4863e11b}

## Commands Used
```bash
file fixme2.py
nano fixme2.py
python3 fixme2.py