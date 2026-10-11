# Glitch Cat

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** LT 'syreal' Jones
- **Platform:** picoCTF
- **Event:** Beginner picoMini 2022
- **Connection:** Netcat
- **Host:** `chatelaine.cylabacademy.net`
- **Port:** `17986`

## What I Learned

- Learned how ASCII represents characters using numeric values.
- Learned how Python's `chr()` function converts an integer into its corresponding character.
- Learned how to recognize and understand Python code hidden inside a seemingly glitched output.
- Practiced extracting characters from hexadecimal values to reconstruct a flag.
- Learned that understanding the output format can be easier than writing a separate program to process every character.
- Learned to use hints effectively when a challenge approach becomes unnecessarily complicated.

## Approach

1. **Connected to the challenge server**

   Used Netcat to connect to the remote flag-printing service:

       nc chatelaine.cylabacademy.net 17986

2. **Examined the glitched output**

   The server returned a Python expression instead of printing the flag directly:

       'academy{gl17ch_m3_n07_' + chr(0x63) + chr(0x62) + chr(0x63) + chr(0x31) + chr(0x38) + chr(0x61) + chr(0x32) + chr(0x34) + '}'

3. **Tried a manual approach**

   Initially, I created a Python file named `a.py` and attempted to print the characters individually. My first attempt produced an `IndentationError`, which I fixed before successfully printing the characters.

   However, manually extracting the characters was more complicated than necessary.

4. **Used the challenge hints**

   The hints explained that:
   - ASCII is a common character encoding.
   - The glitched output is valid Python code.
   - `Ctrl + C` can be used to close the connection and return to the terminal.

   The key realization was that the output was already a valid Python expression that could be evaluated directly.

5. **Reconstructed the flag using Python**

   Opened the Python interpreter:

       python3

   Then evaluated the expression using `print()`:

       print('academy{gl17ch_m3_n07_' + chr(0x63) + chr(0x62) + chr(0x63) + chr(0x31) + chr(0x38) + chr(0x61) + chr(0x32) + chr(0x34) + '}')

6. **Recovered the flag**

   Python converted each hexadecimal value into its corresponding character and combined the characters with the existing string.

   The final output was:

       academy{gl17ch_m3_n07_cbc18a24}

## Commands / Tools Used

- `nc chatelaine.cylabacademy.net 17986` — connects to the remote challenge service.
- `nano a.py` — creates or edits a Python script.
- `python3 a.py` — executes the Python script.
- `python3` — opens the interactive Python interpreter.
- `print()` — displays the reconstructed flag.
- `chr()` — converts an integer character code into its corresponding Unicode character; for these values, the resulting characters match ASCII.
- `Ctrl + C` — interrupts the running process or closes the active challenge interaction.

## Key Concepts

### 1. ASCII and Character Codes

ASCII represents characters using numeric codes. For example, the hexadecimal value `0x63` corresponds to the character `c`.

### 2. Hexadecimal Values

Hexadecimal is a base-16 number system that uses the digits `0–9` and letters `a–f`.

In Python, a number beginning with `0x` is interpreted as hexadecimal.

Examples:

- `0x63` → `c`
- `0x62` → `b`
- `0x31` → `1`
- `0x38` → `8`

### 3. Python's `chr()` Function

The `chr()` function converts an integer into its corresponding character.

For example:

    print(chr(0x63))

Output:

    c

The challenge used multiple `chr()` calls to hide part of the flag in character codes.

### 4. String Concatenation

Python uses the `+` operator to join strings.

For example:

    print('Hello ' + 'World')

Output:

    Hello World

The challenge combined the initial part of the flag, the characters returned by `chr()`, and the closing brace.

### 5. Valid Python Expressions

The glitched output looked unusual, but it was valid Python code. Instead of manually decoding every character, I could evaluate the expression and let Python reconstruct the string.

## Result

Successfully decoded the glitched Python expression and recovered the flag.

## Flag

academy{gl17ch_m3_n07_cbc18a24}