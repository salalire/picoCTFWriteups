# HashingJobApp

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** LT 'syreal' Jones
- **Platform:** picoCTF
- **Event:** Beginner picoMini 2022
- **Connection:** Netcat
- **Host:** `xebec.cylabacademy.net`
- **Port:** `31008`

## What I Learned

- Learned how MD5 hashing works and how to generate an MD5 hash from a text string.
- Learned how to use online tools or Python to calculate MD5 hashes quickly.
- Practiced interacting with a remote service using Netcat.
- Learned that hashes must match exactly, including capitalization, spaces, and punctuation.
- Learned to respond quickly because the challenge has a time limit.
- Understood that automating repetitive hashing tasks can save time and reduce mistakes.

## Approach

1. **Connected to the challenge server**

   Used Netcat to connect to the remote service:

       nc xebec.cylabacademy.net 31008

2. **Examined the challenge prompt**

   The server requested the MD5 hash of a text string between single quotes, excluding the quotes.

   Example prompt:

       Please md5 hash the text between quotes, excluding the quotes: 'Hollywood'

3. **Initially tried answering manually**

   At first, I was unsure how to generate the hashes quickly. I interrupted the connection and reconnected to try again.

   When I received the prompt for `Confucius`, I ran out of time before submitting an answer.

4. **Generated the MD5 hashes**

   For the text `Hollywood`, the correct MD5 hash was:

       1ac441036f927b9815ba1137464ee064

   For the text `a full moon`, the correct MD5 hash was:

       3dbbee596fa3666609f8bcff87bb3df4

   I entered the corresponding hashes into the challenge service.

5. **Answered the prompts correctly**

   The service confirmed each submitted hash with the message:

       Correct.

   I continued answering the prompts until the challenge displayed the flag.

6. **Retrieved the flag**

   After successfully completing the hashing task, the server returned the flag.

## Commands / Tools Used

- `nc xebec.cylabacademy.net 31008` — connects to the remote challenge service.
- `Ctrl + C` — interrupts the active connection.
- **MD5 hashing** — converts the provided text into a 128-bit hash, commonly displayed as 32 hexadecimal characters.

## Key Concepts

### 1. What Is Hashing?

Hashing is the process of converting input data into a fixed-length output using a hash function.

For example, an MD5 hash of `Hollywood` is:

    1ac441036f927b9815ba1137464ee064

Even a small change in the input, such as changing a letter's capitalization or adding a space, produces a different hash.

### 2. MD5 Hashing

MD5 is a hash function that produces a 128-bit digest, usually represented as a 32-character hexadecimal string.

Although MD5 is useful for understanding hashing and completing this challenge, it is not considered secure for modern password storage or collision-resistant applications.

### 3. Netcat

Netcat (`nc`) is a command-line utility used to connect to network services. In this challenge, it provided an interactive connection to the remote hashing application.

### 4. Time-Limited Challenges

The challenge required generating and submitting hashes quickly. Preparing a reliable hashing method before reconnecting would make it easier to respond within the time limit.

### 5. Automation

A small Python script or a command-line utility can calculate MD5 hashes automatically. This is more efficient than manually calculating each hash and helps avoid errors.

## Result

Successfully connected to the remote hashing service, submitted the requested MD5 hashes, and completed the challenge.

## Flag

academy{4ppl1c4710n_r3c31v3d_8c3fe27c}