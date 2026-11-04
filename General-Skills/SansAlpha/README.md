# SansAlpha

## Category
General Skills

## Difficulty
Medium

## Challenge Information
- **Platform:** picoCTF
- **Year:** 2024
- **Author:** syreal

## Overview
The challenge provides SSH access to a restricted Linux environment where the keyboard only allows numbers and most symbols. The objective is to retrieve the flag without using alphabetic characters in commands.

This challenge focuses on Linux shell wildcards, pathname expansion, and finding alternative ways to execute commands when typing letters is restricted.

## Approach

### 1. Connect to the Remote Server

First, I connected to the challenge server using SSH:

    ssh -p 14539 ctf-player@chatelaine.cylabacademy.net

Password:

    13792798

After successfully connecting, I was presented with the restricted `SansAlpha` shell.

### 2. Understand the Shell Restrictions

Since alphabetic characters were unavailable, I needed to find a way to execute commands using symbols and wildcards.

I experimented with wildcard patterns:

    *
    */*
    /*

These attempts helped me understand how the shell expands wildcard expressions into matching filenames and directories.

For example:
- `*` matches entries in the current directory.
- `*/*` matches entries inside directories in the current directory.
- `/*` matches entries directly under the root directory.

### 3. Locate Executable Commands Using Wildcards

Linux commands are stored in directories such as `/bin`.

Instead of typing a command name, I used wildcard patterns to match executable filenames.

For example:

    /*/???

This pattern expanded to executable paths with three-character names, including `/bin/awk`.

I then experimented with patterns that matched commands based on their filename lengths.

### 4. Identify the Base64 Utility

I eventually used:

    /*/??????

This matched multiple six-character executable names, including `base32` and `basenc`, so the command failed because more than one executable was matched.

Next, I narrowed the pattern to target the Base64 utility:

    /*/????64 */*

This matched `/bin/base64`, but also expanded the second argument into multiple filenames.

I refined the pattern further:

    /*/???[!\_]64 */*

The `[!\_]` character class excluded an underscore, narrowing the matching filenames.

Finally, I used:

    /*/???[!\_]64 */????.*

This successfully selected the Base64 executable and a matching file from the challenge directory.

The command produced the following encoded output:

    cmV0dXJuIDAgYWNhZGVteXs3aDE1X211MTcxdjNyNTNfMTVfbTRkbjM1NV9iZDQ5ZWUzZn0=

### 5. Decode the Base64 Output

After leaving the SSH session, I decoded the output on my local machine:

    echo "cmV0dXJuIDAgYWNhZGVteXs3aDE1X211MTcxdjNyNTNfMTVfbTRkbjM1NV9iZDQ5ZWUzZn0=" | base64 -d

The decoded result was:

    return 0 academy{7h15_mu171v3r53_15_m4dn355_bd49ee3f}

The flag was successfully retrieved.

## Commands and Tools Used

| Command / Pattern | Purpose |
|---|---|
| `ssh -p` | Connect to the remote challenge server using a specific port. |
| `*` | Match filenames in the current directory. |
| `*/*` | Match entries inside directories. |
| `/*` | Match entries directly under the root directory. |
| `???` | Match filenames containing exactly three characters. |
| `??????` | Match filenames containing exactly six characters. |
| `[!\_]` | Match a character other than an underscore. |
| `echo` | Print the encoded output. |
| `base64 -d` | Decode Base64-encoded data. |

## Key Concepts Learned

### 1. Shell Wildcards
Wildcards allow us to match filenames without typing their complete names. The shell expands these patterns before executing a command.

### 2. Pathname Expansion
A pattern such as `/*/???` can match multiple executable paths. This makes wildcard expansion useful when command names cannot be typed directly.

### 3. Character Classes
Character classes such as `[abc]` and `[!abc]` allow more precise filename matching.

### 4. Command Execution Through Wildcards
Linux shell commands can be invoked through matching executable paths rather than explicitly typing their names.

### 5. Base64 Encoding and Decoding
Base64 represents binary or textual data using printable characters. The `base64 -d` command decodes Base64 data back into its original form.

## Lessons Learned

- Alphabetic characters are not always necessary to interact with a Linux shell.
- Shell wildcards can be used to locate and execute commands.
- Understanding pathname expansion helps when working in restricted environments.
- Combining wildcards and character classes makes filename matching more precise.
- Base64 decoding is useful for retrieving information hidden in encoded output.

## Flag

    academy{7h15_mu171v3r53_15_m4dn355_bd49ee3f}