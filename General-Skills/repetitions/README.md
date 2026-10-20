# Repetitions

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Theoneste Byagutangaza
- **Platform:** picoCTF
- **Year:** 2023
- **Challenge Name:** Repetitions
- **File:** `enc_flag`
- **Working Directory:** `~/sald`

## What I Learned

- How to recognize and decode Base64-encoded data.
- How to identify and decode multiple layers of Base64 encoding.
- How to use Linux command-line tools to decode encoded text.
- How to recognize when decoded output is still encoded and requires further processing.
- How to reconstruct a flag by repeatedly decoding data until readable text appears.

## Approach

### 1. Examine the Challenge File

The challenge provided a file named `enc_flag`. I used the `cat` command to display its contents.

    cat enc_flag

The output looked like a long string of random characters. This suggested that the content was encoded rather than ordinary readable text.

### 2. Decode the First Layer

I used the `base64` command with the `-d` option to decode the content.

    echo "ENCODED_TEXT" | base64 -d

- `echo` outputs the encoded string.
- `|` passes the output to the next command.
- `base64` processes Base64-encoded data.
- `-d` tells Base64 to decode the input.

The output was another encoded string rather than the flag.

### 3. Repeat the Decoding Process

I repeated the Base64 decoding process on the output from each previous step.

Each decoding operation revealed another layer of encoded data. Since the result continued to look like Base64, I decoded it again.

The process continued until the output became readable.

### 4. Recover the Flag

After repeatedly decoding the nested Base64 strings, the final output revealed the flag:

    academy{base64_n3st3d_dic0d!n8_d0wnl04d3d_9f9309ce}

## Commands / Tools Used

- `cat enc_flag` — displayed the contents of the challenge file.
- `echo "ENCODED_TEXT"` — printed encoded text to the terminal.
- `base64 -d` — decoded Base64-encoded data.
- `|` — piped the output of one command into another.

## Key Concepts

### Base64 Encoding

Base64 is an encoding scheme that represents binary data using a set of printable characters. It is commonly used to represent data in text-based systems.

Base64 is an encoding method, not encryption. It does not require a secret key to reverse.

### Nested Base64 Encoding

Nested encoding occurs when data is encoded multiple times. Decoding one layer reveals the encoded content of the next layer.

For this challenge, the output of each decoding step had to be decoded again until the original readable message was recovered.

### Recognizing Encoded Data

Base64 strings commonly contain uppercase and lowercase letters, digits, and sometimes `+`, `/`, and `=` padding characters.

Recognizing these patterns can help identify possible Base64-encoded data during CTF challenges.

## Lessons Learned

- Do not assume that decoding a string once will reveal the final answer.
- Inspect the output after every decoding operation.
- If the output still resembles Base64, try decoding it again.
- Understand what each command does instead of simply repeating commands without checking their output.
- Repeated encoding and decoding is a common technique in introductory CTF challenges.

## Result

Successfully decoded the nested Base64 content and recovered the flag.

## Flag

academy{base64_n3st3d_dic0d!n8_d0wnl04d3d_9f9309ce}