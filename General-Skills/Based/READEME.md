# Based

## Category
General Skills

## Difficulty
Medium

## Challenge Information
- **Platform:** picoCTF
- **Competition:** picoCTF 2019
- **Authors:** Alex Fulton and Daniel Tunitis

## Overview

The challenge focuses on understanding different data encoding formats, including binary, octal, and hexadecimal.

After connecting to the remote service using Netcat, the program presents encoded values and asks the user to convert them into readable words.

The objective is to correctly identify each encoding format, decode the values, and submit the corresponding words within the 45-second time limit.

## Approach

### 1. Connect to the Remote Service

I started by connecting to the challenge server using Netcat:

    nc chatelaine.cylabacademy.net 32605

The application displayed:

    Let us see how data is stored

    Please give the 01100011 01101000 01100001 01101001 01110010 as a word.

    ...you have 45 seconds.....

    Input:

The program expected me to decode the provided values and enter the resulting word.

### 2. Decode Binary Values

The first encoding format encountered was binary.

For example:

    01100011 01101000 01100001 01101001 01110010

Each group represents an 8-bit binary value corresponding to an ASCII character.

The binary values can be converted into decimal and then interpreted using the ASCII character table.

The decoded word was:

    chair

I entered `chair` into the program.

### 3. Decode Octal Values

The next question presented values in octal (base 8):

    Please give me the 164 145 163 164 as a word.

Each group represents an ASCII character encoded using its octal value.

The decoded characters are:

| Octal | ASCII Character |
|---|---|
| `164` | t |
| `145` | e |
| `163` | s |
| `164` | t |

The resulting word was:

    test

However, my first attempt timed out because I could not decode and submit the answer within the 45-second limit.

### 4. Decode Additional Binary Values

I reconnected to the service and received another binary question:

    01100011 01101111 01101110 01110100 01100001 01101001 01101110 01100101 01110010

After converting each binary group into its corresponding ASCII character, the result was:

    container

I submitted the answer:

    container

The next question contained octal values:

    154 151 155 145

These values represent:

| Octal | ASCII Character |
|---|---|
| `154` | l |
| `151` | i |
| `155` | m |
| `145` | e |

The decoded word was:

    lime

I was able to identify the answer, but the session timed out before I could submit it successfully.

### 5. Decode Hexadecimal Values

In another attempt, the program presented:

    70656172

This value was encoded in hexadecimal (base 16).

I separated it into two-character groups:

    70 65 61 72

Each pair represents one ASCII character:

| Hexadecimal | ASCII Character |
|---|---|
| `70` | p |
| `65` | e |
| `61` | a |
| `72` | r |

The decoded word was:

    pear

This attempt also demonstrated why identifying the encoding format before decoding is important.

### 6. Complete the Challenge

After reconnecting again, I received the following binary value:

    01110011 01110101 01100010 01101101 01100001 01110010 01101001 01101110 01100101

I decoded it as:

    submarine

I submitted the answer:

    submarine

The next question contained octal values:

    154 151 155 145

I converted them into ASCII characters:

    lime

After submitting `lime`, the program presented a hexadecimal value:

    7461626c65

I separated it into pairs:

    74 61 62 6c 65

The corresponding ASCII characters were:

| Hexadecimal | ASCII Character |
|---|---|
| `74` | t |
| `61` | a |
| `62` | b |
| `6c` | l |
| `65` | e |

The resulting word was:

    table

I entered:

    table

The application confirmed that I had successfully completed the challenge:

    You've beaten the challenge
    Flag: academy{learning_about_converting_values_c51c32E4}

## Commands and Tools Used

| Command / Tool | Purpose |
|---|---|
| `nc` | Connect to the remote challenge service. |
| `nc chatelaine.cylabacademy.net 32605` | Establish a connection to the challenge server. |
| Python | Convert binary, octal, and hexadecimal values into readable text. |
| ASCII table | Map numeric character codes to their corresponding characters. |

## Key Concepts Learned

### 1. Binary Encoding

Binary is a base-2 number system that uses only two digits:

- `0`
- `1`

In this challenge, each group of eight bits represented one ASCII character.

For example:

    01100011 = c

### 2. Octal Encoding

Octal is a base-8 number system that uses digits from `0` to `7`.

Each octal value represented an ASCII character.

For example:

    154 = l

### 3. Hexadecimal Encoding

Hexadecimal is a base-16 number system that uses:

- Digits `0–9`
- Letters `a–f`

In ASCII hexadecimal encoding, each byte is represented by two hexadecimal digits.

For example:

    74 = t

### 4. ASCII Encoding

ASCII (American Standard Code for Information Interchange) is a character encoding standard that maps numeric values to characters.

The challenge used ASCII values represented in different number systems.

Understanding the relationship between binary, octal, hexadecimal, and ASCII made it possible to decode the provided words.

### 5. Time Constraints

The challenge provided only 45 seconds to answer the questions.

My initial attempts timed out because I needed more time to identify the encoding format and convert the values.

This made it important to understand the conversion process before reconnecting.

## Python Conversion Techniques

Python provides built-in functions that make these conversions easier.

For binary:

    int('01100011', 2)

For octal:

    int('154', 8)

For hexadecimal:

    int('74', 16)

To convert a numeric value into its corresponding ASCII character:

    chr(int('01100011', 2))

To decode an entire hexadecimal string:

    bytes.fromhex('7461626c65').decode()

These techniques are useful when solving encoding challenges under time constraints.

## Lessons Learned

- Always identify the encoding format before attempting to decode a value.
- Binary, octal, and hexadecimal are different number systems that can represent the same ASCII characters.
- Python provides convenient built-in functions for converting between number systems and text.
- The ASCII character table is useful for understanding how numeric values represent readable characters.
- Time-limited challenges require preparation and familiarity with the conversion techniques.
- Keeping a separate terminal window open for Python conversions can save valuable time while interacting with a remote service.

## Result

Successfully decoded binary, octal, and hexadecimal values into their corresponding ASCII words and completed all questions within the challenge's time limit.

## Flag

    academy{learning_about_converting_values_c51c32E4}