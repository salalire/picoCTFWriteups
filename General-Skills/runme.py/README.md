
# runme.py

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Sujeet Kumar
- **Platform:** picoCTF
- **Event:** picoMini 2022

## What I Learned

- Learned how to download Python scripts from a provided URL using `wget`.
- Practiced navigating directories and organizing challenge files in a Linux environment.
- Learned how to execute Python scripts using the Python 3 interpreter.
- Understood that reviewing a script's purpose and running it can be enough to solve a basic programming challenge.
- Practiced retrieving a flag from a program's output.

## Approach

1. Checked my current working directory using `pwd`.
2. Created a dedicated directory named `sald` to organize the challenge files.
3. Navigated into the directory using `cd sald`.
4. Downloaded the provided Python script using `wget`.

       wget https://challenge-files.cylabacademy.net/library/e4f0c4525ade26a755d6b5c3ce5b220a10c295879c2c3b75385e3a6c9e1ae697/runme.py

5. Verified that the script was downloaded by listing the directory contents.

       ls

6. Executed the script using Python 3.

       python3 runme.py

7. The program ran successfully and printed the flag.

## Commands / Tools Used

- `pwd` — display the current working directory.
- `mkdir` — create a directory.
- `cd` — navigate between directories.
- `wget` — download the challenge script.
- `ls` — list directory contents.
- `python3` — execute the Python script.

## Key Concept

Python scripts can be executed directly through the Python interpreter without needing to make them executable.

The command:

    python3 runme.py

instructs Python 3 to execute the code contained in `runme.py`.

In this challenge, the task was to download and run the provided script rather than develop a separate solution.

## Result

Successfully downloaded and executed the challenge script, which printed the flag.

## Flag

academy{run_s4n1ty_run}