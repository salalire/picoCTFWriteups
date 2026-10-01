# bytemancy 0

## Category

General Skills

## Difficulty

Easy

## What I Learned

- Learned how to inspect a challenge's source code to understand its input requirements.
- Learned how hexadecimal escape sequences represent characters in Python.
- Learned that `\x65` represents the ASCII character `e`.
- Learned how Python string multiplication can generate repeated characters.
- Practiced using Python to automate input instead of entering repetitive data manually.
- Learned how to send programmatically generated input to a remote service using Netcat.
- Improved my ability to read challenge source code and identify the exact condition required to obtain the flag.

## Approach

1. Downloaded the provided `app.py` source code using `wget`.

       wget https://challenge-files.cylabacademy.net/library/a01594863b05e64afea8a17cedaefe2f3561d9bb1d869c1b282d9d732dc61c0c/app.py

2. Checked the downloaded file to confirm that it was a Python script.

       file app.py.1

3. Opened the source code and inspected how the application validates the user's input.

4. Found the important comparison:

       if user_input == "\x65\x65\65":

5. Interpreted `\x65` as a hexadecimal ASCII escape sequence.

       \x65 → 0x65 → decimal 101 → ASCII 'e'

6. Therefore, the program expects the character `e` repeated exactly `3` times.

7. Created a small Python script to generate the required input and send it to the challenge service using Netcat.

       import subprocess

       data = "\x65" * 3

       subprocess.run(
           ["nc", "chatelaine.cylabacademy.net", "46209"],
           input=data + "\n",
           text=True
       )

8. Ran the Python script and the server accepted the generated input.

9. The challenge returned the flag.

## Commands / Tools Used

- `wget`
- `file`
- `nano`
- Python 3
- Netcat (`nc`)
- ASCII
- Hexadecimal escape sequences

## Key Concept

The most important part of the challenge was reading the source code instead of guessing the required input.

The application checks:

       user_input == "\x65"*3

In Python:

       \x65

is a hexadecimal escape sequence representing the byte:

       0x65

which is decimal:

       101

and corresponds to the ASCII character:

       e

The `*3` operation repeats that character 3 times.

Therefore, the required input is:

       eee.. [3 characters]

The challenge description displays the decimal representation `101`, but the source code reveals that the application actually compares the input against the character represented by hexadecimal `\x65`.

## Solution Strategy

The general strategy for this challenge was:

       Read source code
              ↓
       Find input validation
              ↓
       Interpret \x65
              ↓
       Identify ASCII character 'e'
              ↓
       Repeat it 3 times
              ↓
       Send input with Netcat
              ↓
       Receive flag

## Result

The generated input matched the exact condition in the source code, allowing the challenge server to reveal the flag.

## Flag

academy{pr1n74813_ch4r5_b44ec13d}