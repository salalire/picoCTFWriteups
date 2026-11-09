# MultiCode

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Yahaya Meddy
- **Platform:** picoCTF
- **Year:** 2026
- **File:** `message.txt`

## What I Learned

- Learned how to identify and decode multiple layers of text encoding.
- Learned how Base64, hexadecimal, and ROT13 transform readable text.
- Practiced using Linux command-line tools to decode encoded messages.
- Learned how to use CyberChef to decode multiple encoding layers efficiently.
- Understood the difference between encoding and encryption.
- Improved my ability to analyze suspicious text and follow clues to uncover a hidden flag.

## Approach

1. **Downloaded the challenge file**

   Downloaded `message.txt` from the challenge's provided link and read its contents to inspect the suspicious message.

2. **Identified the first encoding layer**

   After examining the message, I recognized that the first layer used Base64 encoding.

   Base64 converts data into a text representation using a set of 64 characters. It is an encoding scheme, not encryption.

3. **Decoded the message using the command line**

   Used a Linux command-line tool to decode the first Base64 layer and reveal the next encoded text.

4. **Identified the remaining encoding layers**

   By examining the decoded output, I recognized additional encoding methods:
   - **Hexadecimal:** Represents data using hexadecimal characters.
   - **ROT13:** Replaces each English letter with the letter 13 positions away in the alphabet.

5. **Used CyberChef to decode the remaining layers**

   Opened CyberChef in a browser and applied the appropriate decoding operations to the intermediate output.

   By peeling back the encoding layers one at a time, I gradually recovered the readable message.

6. **Recovered the flag**

   After decoding the nested layers, I obtained the final flag:

       academy{nested_enc0ding_9c4d05f7}

## Commands / Tools Used

- `cat message.txt` — displays the contents of the downloaded message file.
- `base64 -d` — decodes Base64-encoded data.
- **CyberChef** — applies decoding operations such as From Hex and ROT13.
- **Linux terminal** — used to inspect the file and decode the initial layer.

## Key Concepts

### 1. Base64 Encoding

Base64 converts binary data or text into a printable representation using 64 possible characters.

Linux example:

    echo 'SGVsbG8=' | base64 -d

Output:

    Hello

### 2. Hexadecimal Encoding

Hexadecimal uses 16 symbols (`0–9` and `a–f`) to represent values. Text can be represented as hexadecimal byte values and decoded back into readable characters.

### 3. ROT13

ROT13 is a simple letter substitution technique that shifts each English letter 13 positions through the alphabet.

Example:

    Hello → Uryyb

Applying ROT13 a second time restores the original text.

### 4. Nested Encoding

Nested encoding means that data has been encoded multiple times using different encoding methods.

To recover the original message, each layer must be identified and decoded in the correct order.

### 5. Encoding vs. Encryption

- **Encoding** changes how information is represented and can generally be reversed without a secret key.
- **Encryption** protects information using a cryptographic algorithm and typically requires a key to decrypt it.

This challenge used encoding techniques rather than encryption.

## Result

Successfully identified and decoded the Base64, hexadecimal, and ROT13 layers using Linux command-line tools and CyberChef to recover the hidden flag.

## Flag

academy{nested_enc0ding_9c4d05f7}