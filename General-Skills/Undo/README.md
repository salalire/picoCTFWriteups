# Text Transformations

## Category

General Skills

## Difficulty

Medium

## What I Learned

- Learned how to reverse a series of Linux text transformations step by step.
- Used `base64 -d` to decode Base64.
- Used `rev` to reverse text.
- Used `tr` to replace characters and undo transformations.
- Learned that transformations must be reversed in the opposite direction.

## Approach

1. Connected to the remote service using `nc`.
2. Decoded the Base64 text using `base64 -d`.
3. Reversed the text using `rev`.
4. Replaced `-` with `_` using `tr '-' '_'`.
5. Continued reversing each transformation based on the provided hints.
6. Recovered the original flag.

## Commands Used

    nc foggy-cliff.picoctf.net 59956
    base64 -d
    rev
    tr '-' '_'

## Flag

picoCTF{Revers1ng_t3xt_Tr4nsf0rm@t10ns_0ea42cd0}
