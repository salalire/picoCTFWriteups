# Useless

## Category

General Skills

## Difficulty

Medium

## Challenge Information

- **Author:** Loic Shema
- **Platform:** picoCTF
- **Year:** 2023
- **Challenge Name:** Useless
- **Target Host:** `chatelaine.cylabacademy.net`
- **SSH Port:** `33727`
- **Username:** `picoplayer`
- **File:** `useless`

## What I Learned

- How to connect to a remote Linux machine using SSH.
- How to inspect a Bash script using `cat`.
- How to understand command-line arguments in shell scripts.
- How to use the `man` command to read a program's manual.
- How to discover useful information from documentation that is not immediately obvious from a script.
- How to retrieve a flag by exploring a program and its associated documentation.

## Approach

### 1. Connect to the Remote Machine

I connected to the challenge server using SSH.

    ssh -p 33727 picoplayer@chatelaine.cylabacademy.net

After entering the provided password, I successfully accessed the remote Linux machine.

### 2. Find the Challenge Script

I listed the files in the home directory.

    ls

The output showed a file named:

    useless

### 3. Inspect the Script

I used `cat` to examine the contents of the script.

    cat useless

The script was a Bash calculator that accepted three command-line arguments.

Its supported operations were:

- `add` — addition
- `sub` — subtraction
- `mul` — multiplication
- `div` — division

The script first checked whether exactly three arguments had been provided. If not, it displayed:

    Read the code first

It then checked the first argument to determine which mathematical operation to perform.

This helped me understand the script's expected input format.

### 4. Test the Script's Behavior

I initially tried an incorrect command:

    bash ped 12 34

The shell returned an error because a file named `ped` did not exist.

Next, I tried:

    bash useless pwd 12 12

The script returned:

    Read the manual

This happened because `pwd` was not one of the supported operations.

The response suggested that the program's manual contained additional information.

### 5. Read the Manual

I executed:

    man useless

The manual described the script's supported operations and provided usage examples.

More importantly, the manual contained the flag itself.

This demonstrated that reading documentation can reveal information that is not apparent from the program's source code.

### 6. Retrieve the Flag

The manual revealed the following flag:

    academy{us3l3ss_ch4ll3ng3_3xpl0it3d_4318}

## Commands / Tools Used

- `ssh -p 33727 picoplayer@chatelaine.cylabacademy.net` — connected to the remote challenge machine.
- `ls` — listed files in the home directory.
- `cat useless` — displayed the Bash script's source code.
- `bash useless pwd 12 12` — tested an unsupported operation.
- `man useless` — opened the program's manual and revealed the flag.

## Key Concepts

### Bash Command-Line Arguments

Bash scripts can receive arguments when executed.

In this challenge:

- `$1` represented the first argument, which specified the operation.
- `$2` represented the first number.
- `$3` represented the second number.
- `$#` represented the total number of arguments supplied.

The script used these values to determine which calculation to perform.

### Conditional Statements

The script used `if`, `elif`, and `else` statements to select the appropriate mathematical operation.

For example, when the first argument was `add`, the script added the second and third arguments.

### Manual Pages

The `man` command displays documentation for commands and programs installed on a Linux system.

Manual pages can contain usage instructions, examples, descriptions, and other information useful for understanding a program.

In this challenge, the manual was the key to finding the flag.

### Exploring Linux Systems

A useful approach to command-line challenges is to inspect available files, examine scripts, test their expected inputs, and consult their documentation.

Sometimes, the intended solution is hidden in a program's manual rather than in its source code.

## Lessons Learned

- Inspect unfamiliar scripts before executing them.
- Understand how command-line arguments affect a program's behavior.
- Pay attention to error messages and unexpected output because they can provide useful clues.
- Use `man` to discover documentation for commands and custom programs.
- Do not overlook documentation when investigating a Linux challenge.
- The simplest solution may involve exploring the environment rather than exploiting a complex vulnerability.

## Result

Successfully inspected the Bash calculator script, tested its behavior, and discovered the flag in its manual page.

## Flag

academy{us3l3ss_ch4ll3ng3_3xpl0it3d_4318}