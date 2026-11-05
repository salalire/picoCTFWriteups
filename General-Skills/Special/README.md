# Special

## Category
General Skills

## Difficulty
Medium

## Challenge Information
- **Platform:** picoCTF
- **Year:** 2023
- **Author:** LT 'syreal' Jones
- **Challenge Name:** Special

## Overview

The Special challenge introduces a restricted Linux shell interface that automatically modifies commands before executing them.

The challenge description explains that the interface automatically corrects spelling and capitalization. However, this behavior makes normal Linux commands difficult to execute because command names and arguments can be changed unexpectedly.

The objective was to understand how the special shell processes user input and find a way to execute commands without being affected by its automatic modifications.

The flag was stored in:

    ./blargh/flag.txt

## Approach

### 1. Connect to the Remote Server

I started by connecting to the challenge server through SSH:

    ssh -p 23983 ctf-player@chatelaine.cylabacademy.net

Password:

    647e170e

After successfully connecting, I was presented with the restricted shell:

    Special$

### 2. Understand the Special Shell Behavior

I first tried to execute multiple commands using the normal Linux shell syntax.

My first attempt was:

    clear & find

However, the shell transformed the input:

    Clear & find

The command failed with:

    sh: 1: Clear: not found

This showed that the interface automatically changed `clear` into `Clear`.

Linux commands are case-sensitive, so `clear` and `Clear` are treated as different command names.

This was an important discovery: the shell was modifying my commands before passing them to the underlying shell.

### 3. Locate the Flag File

I used the `find` command to inspect the directory structure.

The output showed:

    .
    ./blargh
    ./blargh/flag.txt
    ./.cache
    ./.cache/motd.legal-displayed

This revealed that the flag was stored inside the `blargh` directory.

The target file was:

    ./blargh/flag.txt

### 4. Try Reading the Flag Directly

After locating the file, I tried to read it using `cat`:

    clear $ cat ./blargh/flag.txt

The special interface transformed the input into:

    Clear $ cat ./blargh/flag.txt

It failed because `Clear` was not a valid command.

I then tried:

    $cat /blargh/flag.txt

The interface transformed this into:

    Cat /blargh/flag.txt

Again, the command failed because the command name was capitalized.

These attempts confirmed that ordinary commands were being modified automatically.

### 5. Understand the Special Character Behavior

Next, I experimented with the `&` character:

    & cat /blargh/flag.txt

The shell returned:

    Syntax error: "&" unexpected

This showed that the special interface was not simply executing the input exactly as I typed it. The input was being processed before reaching the underlying shell.

I also tried:

    clear & ./blargh/flag.txt

The output included:

    sh: 1: Clear: not found
    sh: 1: ./blargh/flag.txt: Permission denied

This confirmed that directly executing the flag file was not the correct approach.

### 6. Successfully Bypass the Command Modification

After experimenting with different inputs, I tried the following command:

    Clear & cat ./blargh/flag.txt

The special interface displayed:

    Clear & cat ./blargh/flag.txt

Although `Clear` was still not found, the important part was that the command after `&` successfully executed.

The shell returned:

    sh: 1: Clear: not found
    academy{5p311ch3ck_15_7h3_w0r57_c78cfa94}

This revealed the flag.

The key was using `&` to separate the invalid command from the command that actually read the flag. The second command was executed successfully even though the first command failed.

## Commands and Tools Used

| Command / Symbol | Purpose |
|---|---|
| `ssh -p` | Connect to the remote challenge server using a specific port. |
| `clear` | Attempt to clear the terminal. |
| `find` | Search for files and directories. |
| `cat` | Display the contents of a file. |
| `&` | Execute commands asynchronously in the shell. |
| `./blargh/flag.txt` | Specify the location of the flag file. |

## Key Concepts Learned

### 1. Linux Commands Are Case-Sensitive

Linux distinguishes between uppercase and lowercase characters.

For example:

    cat

and:

    Cat

are different command names.

This explains why the automatic capitalization caused normal commands to fail.

### 2. Shell Command Processing

Before executing a command, a shell processes the input and interprets special characters, operators, and arguments.

In this challenge, the special interface modified the input before it reached the underlying shell.

### 3. The Ampersand (`&`) Operator

In a normal Linux shell, `&` runs a command in the background.

For example:

    sleep 10 &

starts `sleep` in the background, allowing the shell to continue accepting commands.

In this challenge, the ampersand was useful for separating the unsuccessful first command from the command that successfully read the flag.

### 4. File Permissions

Attempting to execute the flag file directly resulted in:

    Permission denied

This demonstrated that having a file's location does not necessarily mean it can be executed.

To display a text file, a command such as `cat` is more appropriate than trying to execute the file.

### 5. Understanding Restricted Shells

Restricted or modified shell environments can change how commands are interpreted.

Understanding the shell's behavior through controlled experiments can reveal ways to interact with the underlying system.

## Lessons Learned

- Always inspect unfamiliar shell environments before assuming they behave like a normal Bash shell.
- Linux command names are case-sensitive.
- Automatic command modification can interfere with normal command execution.
- Special shell characters can change how commands are interpreted.
- The `find` command is useful for locating files when their exact location is unknown.
- File permissions determine whether a file can be read or executed.
- Experimenting with shell behavior can help solve restricted-environment challenges.

## Result

Successfully bypassed the Special shell's command modification behavior and retrieved the flag from `./blargh/flag.txt`.

## Flag

    academy{5p311ch3ck_15_7h3_w0r57_c78cfa94}