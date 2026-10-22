# Codebook

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** LT 'syreal' Jones
- **Platform:** picoCTF
- **Year:** picoMini 2022
- **Challenge Name:** Codebook
- **Files:** `code.py`, `codebook.txt`
- **Working Directory:** `~/sald`

## What I Learned

- How to execute Python scripts using `python3`.
- How to inspect Python source code to understand how a program works.
- How to use `wget` to download challenge files.
- How external text files can provide data required by a Python program.
- How to solve a challenge by running a provided script with its required resources.

## Approach

### 1. Navigate to the Working Directory

I navigated to my `sald` directory, where I planned to download and run the challenge files.

    cd ~/sald

I checked the existing files and removed the previous challenge files to keep the directory organized.

### 2. Download the Challenge Files

I downloaded `code.py` using `wget`.

    wget https://challenge-files.cylabacademy.net/library/3fb494d187a470eb95bf47ca5078ef3bbb640bd1ebe57128a4e67bc861026c16/code.py

Next, I downloaded `codebook.txt`.

    wget https://challenge-files.cylabacademy.net/library/3fb494d187a470eb95bf47ca5078ef3bbb640bd1ebe57128a4e67bc861026c16/codebook.txt

I verified that both files were present.

    ls

The directory contained:

- `code.py`
- `codebook.txt`

### 3. Identify the Python Script

I used the `file` command to inspect the script.

    file code.py

The output identified it as a Python script containing ASCII text.

This confirmed that the file was a script that could be executed with Python.

### 4. Inspect the Source Code

I opened the Python script using `nano`.

    nano code.py

Inspecting the source code helps explain what the program does and how it uses the accompanying `codebook.txt` file.

The challenge instructions specifically required running `code.py` in the same directory as `codebook.txt`, so I kept both files together.

### 5. Execute the Script

I ran the Python script using Python 3.

    python3 code.py

The program executed successfully and printed the flag.

## Commands / Tools Used

- `cd ~/sald` — navigated to the working directory.
- `rm -rf drop-in` — removed the previous challenge directory.
- `rm challenge.zip` — removed the previous challenge archive.
- `wget URL` — downloaded the challenge files.
- `ls` — listed the files in the directory.
- `file code.py` — identified the type of file.
- `nano code.py` — opened the Python script for inspection.
- `python3 code.py` — executed the challenge script.

## Key Concepts

### Python Script Execution

Python scripts contain instructions that the Python interpreter executes.

The command `python3 code.py` instructs Python 3 to execute the code contained in `code.py`.

### External Data Files

Programs sometimes depend on external files to obtain information or perform their tasks.

In this challenge, `codebook.txt` was provided alongside `code.py`. Keeping both files in the same directory followed the challenge's instructions.

### Source Code Inspection

Inspecting source code before execution helps you understand a program's behavior, identify its dependencies, and learn how it produces its output.

## Lessons Learned

- Read the challenge instructions carefully before executing a program.
- Download all required files and keep them in the expected directory.
- Inspect unfamiliar source code to understand its behavior.
- Use `python3` to execute Python scripts in a Linux environment.
- Running the provided program can be the intended solution when a challenge supplies the necessary code and resources.

## Result

Successfully downloaded the challenge files, inspected the Python script, and executed it to retrieve the flag.

## Flag

academy{c0d3b00k_455157_570b049a}