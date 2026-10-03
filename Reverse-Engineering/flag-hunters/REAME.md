
# Flag Hunters

## Category

Reverse Engineering

## Difficulty

Easy

## Challenge Information

- **Author:** syreal
- **Platform:** picoCTF
- **Year:** 2025

## What I Learned

- Learned how to inspect Python source code to understand program control flow.
- Learned how functions and return statements can affect the execution of a program.
- Learned how user-controlled input can influence a program's behavior.
- Practiced interacting with a remote challenge service using Netcat.
- Learned how to analyze a program that processes input and prints different sections of text.
- Improved my debugging skills by testing different inputs and observing the program's output.
- Learned how to identify and access a hidden refrain by understanding the program's execution logic.

## Approach

1. Created a dedicated directory named `salk` to organize the challenge files.

2. Downloaded the provided Python source code using `wget`.

       wget https://challenge-files.cylabacademy.net/library/73506cd1af06b09222f9c694a4d6961b1f959ad76ecf5edaf92c2621694e0613/lyric-reader.py

3. Verified the downloaded file type.

       file lyric-reader.py

4. Opened `lyric-reader.py` using `nano` to inspect the source code and understand how the program processes lyrics and user input.

5. Attempted to run the script locally. The program reported that `flag.txt` was missing, indicating that the local environment did not contain all the files required by the script.

6. Connected to the remote challenge instance using Netcat.

       nc xebec.cylabacademy.net 42535

7. Observed how the service displayed verses and refrains, then experimented with different input values to understand how the program handled them.

8. Examined the program's control flow and tested inputs involving return-related behavior to investigate how execution could be redirected.

9. Identified an input that allowed the program to reach the hidden refrain and display the flag.

10. Recovered the flag from the remote service output.

## Commands / Tools Used

- `pwd` — display the current working directory.
- `mkdir` — create a directory.
- `cd` — navigate between directories.
- `wget` — download the Python source code.
- `ls` — list directory contents.
- `file` — identify the downloaded file type.
- `nano` — inspect and edit source code.
- `python3` — execute Python scripts.
- `nc` — connect to the remote challenge service.

## Key Concepts

### Source Code Analysis

Reading the provided source code helps reveal how the application processes input, selects verses, and decides when to print the refrain.

### Control Flow

Functions, loops, conditions, and return statements determine which parts of a program execute. Understanding these mechanisms helps identify ways to reach code that is not executed during normal operation.

### Input Manipulation

The challenge accepts user input that influences its execution. Testing how the input is interpreted can reveal unexpected behavior and provide a way to reach the hidden section.

## Result

Successfully analyzed the Python program, experimented with the remote service, and triggered the hidden refrain to reveal the flag.

## Flag

academy{70637h3r_f0r3v3r_42783b07}