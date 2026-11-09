# Serpentine

## Category
General Skills

## Difficulty
Medium

## Challenge Information
- **Platform:** picoCTF
- **Year:** 2022
- **Author:** LT 'syreal' Jones
- **Challenge Type:** Beginner picoMini

## Overview

The Serpentine challenge provides a Python script containing a hidden flag.

The program presents a simple menu with three options:

- `a)` Print encouragement
- `b)` Print flag
- `c)` Quit

However, selecting the option to print the flag does not successfully display it. Instead, the program prints a message saying that the `print_flag` function might have been misplaced.

The objective is to inspect the Python source code, understand why the flag-printing functionality is not working, and correct the function call to retrieve the flag.

## Approach

### 1. Download the Challenge File

I started by navigating to my working directory:

    cd ~/sald

Then I downloaded the Python script using `wget`:

    wget https://challenge-files.cylabacademy.net/library/6f4ff467e583437bc55c9d44497b3c0751e233197567e46d19e87f2887bba4e3/serpentine.py

The download completed successfully:

    'serpentine.py' saved

### 2. Verify the Downloaded File

I listed the directory contents:

    ls

Output:

    serpentine.py

Next, I checked the file type:

    file serpentine.py

Output:

    serpentine.py: Python script, ASCII text executable, with very long lines (488)

This confirmed that the downloaded file was a Python script.

### 3. Inspect the Python Source Code

Before trying to solve the challenge through the menu, I opened the source code using:

    nano serpentine.py

While inspecting the script, I noticed that the `print_flag()` function was defined but was not properly called when the user selected option `b`.

This was the main issue preventing the program from displaying the flag through its normal menu option.

The challenge description itself also provided an important hint:

    Find the flag in the Python script!

This suggested that inspecting the source code was an essential part of the solution.

### 4. Execute the Original Python Script

After inspecting the source code, I executed the program:

    python3 serpentine.py

The application displayed an ASCII-art snake and the following menu:

    Welcome to the serpentine encourager!

    a) Print encouragement
    b) Print flag
    c) Quit

    What would you like to do? (a/b/c)

I first selected:

    a

The program printed:

    Look how far you've come!

This confirmed that the encouragement option worked correctly.

### 5. Test the Flag Option

Next, I selected:

    b

The program displayed the flag:

    academy{7h3_r04d_l355_7r4v3l3d_825b10ae}

However, it also printed an error-style message:

    Oops! I must have misplaced the print_flag function! Check my source code!

This behavior confirmed that the flag-printing functionality was not correctly integrated into the menu.

The important discovery was that the flag could be retrieved by examining and correcting the source code rather than relying on the original menu behavior.

### 6. Identify the Problem in the Function Call

The Python script contained a function responsible for printing the flag:

    print_flag()

However, the menu's option-handling logic did not properly invoke this function.

I corrected the source code so that selecting option `b` would call:

    print_flag()

This connected the menu option to the actual flag-printing function.

After saving the modification, I executed the script again:

    python3 serpentine.py

Selecting option `b` successfully invoked the flag-printing functionality.

## Commands and Tools Used

| Command / Tool | Purpose |
|---|---|
| `cd ~/sald` | Navigate to the working directory. |
| `wget` | Download the challenge Python script. |
| `ls` | List files in the working directory. |
| `file serpentine.py` | Identify the downloaded file type. |
| `nano serpentine.py` | Inspect and modify the Python source code. |
| `python3 serpentine.py` | Execute the challenge script. |

## Key Concepts Learned

### 1. Python Function Definition and Function Calls

A function definition describes what a function does, but it does not automatically execute the function.

For example:

    def print_flag():
        print("Flag goes here")

The function must be called to execute its contents:

    print_flag()

This distinction was central to solving the challenge.

### 2. Conditional Statements

Python programs commonly use conditional statements to handle menu selections.

For example:

    if choice == "a":
        print_encouragement()
    elif choice == "b":
        print_flag()
    elif choice == "c":
        exit()

Each condition determines which function or operation should execute.

### 3. Source Code Inspection

Reading source code is an important skill in cybersecurity and software debugging.

Instead of treating a program as a black box, inspecting its implementation can reveal:

- Hidden functions.
- Incorrect function calls.
- Hardcoded information.
- Logic errors.
- Unintended program behavior.

### 4. Debugging Python Programs

The challenge demonstrated how a small mistake in function invocation can prevent an otherwise correctly implemented feature from working as expected.

Understanding the relationship between menu options, conditions, and function calls helps identify these types of problems.

## Lessons Learned

- Always inspect source code when a challenge explicitly suggests finding information inside a script.
- Defining a function does not automatically execute it.
- Menu options need to be connected to the appropriate functions.
- A program can contain the required functionality but still fail because of incorrect control flow.
- Python source code inspection is useful for both debugging and cybersecurity challenges.
- Understanding basic Python functions and conditional statements can solve challenges without requiring complicated tools.

## Result

Successfully inspected and corrected the Python script, identified the missing `print_flag()` function call, and retrieved the challenge flag.

## Flag

    academy{7h3_r04d_l355_7r4v3l3d_825b10ae}