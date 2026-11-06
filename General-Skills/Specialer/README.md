# Specialer

## Category
General Skills

## Difficulty
Medium

## Challenge Information
- **Platform:** picoCTF
- **Year:** 2023
- **Author:** LT 'syreal' Jones et al.
- **Challenge Name:** Specialer

## Overview

Specialer is a Linux shell challenge that provides a restricted command-line environment with a reduced set of available commands.

Unlike the previous **Special** challenge, which modified commands through automatic spelling and capitalization, Specialer removes many familiar Linux utilities entirely.

Commands such as `ls`, `find`, `cat`, `clear`, `sudo`, and `nano` are unavailable.

The objective was to explore the available shell features and discover alternative ways to navigate directories and read files.

The flag was located inside the `ala` directory, in the file `kazam.txt`.

## Approach

### 1. Connect to the Remote Server

I initially experimented with an incorrect SSH port:

    ssh -p 47582 ctf-player@xebec.cylabacademy.net

After that attempt, I used the correct connection details provided by the challenge:

    ssh -p 31064 ctf-player@xebec.cylabacademy.net

Password:

    8d1db23b

After successfully connecting, I received the restricted shell prompt:

    Specialer$

### 2. Explore the Available Commands

My first attempt was to list the files using the familiar Linux command:

    ls

However, the shell returned:

    -bash: ls: command not found

I also tried other standard commands:

    find
    clear
    cat
    sudo -l
    nano

They were unavailable.

This indicated that the environment had a restricted set of executable commands.

### 3. Understand the Available Shell Features

Instead of continuing to depend on unavailable Linux utilities, I explored the shell itself.

I used:

    pwd

The output was:

    /home/ctf-player

To inspect the available shell commands, I entered:

    $PATH

The shell displayed a list of available built-in commands and keywords, including:

    bash
    cd
    echo
    printf
    pwd
    read
    source
    test
    type

This was an important discovery.

Even though external commands such as `ls` and `cat` were unavailable, Bash still provided built-in functionality that could be used to interact with the filesystem.

### 4. Discover the Home Directory Contents

I used the `cd` command without specifying a destination:

    cd

Then I pressed Tab to trigger shell completion.

The shell displayed the available entries:

    .hushlogin
    .profile
    abra/
    ala/
    sim/

This revealed three directories:

- `abra`
- `ala`
- `sim`

Since `ls` was unavailable, tab completion became a useful alternative for discovering directory and file names.

### 5. Explore the Abra Directory

I entered the first directory:

    cd abra

Then I checked my current location:

    pwd

Output:

    /home/ctf-player/abra

I pressed Tab after entering:

    cd cada

The shell displayed matching filenames:

    cadabra.txt
    cadaniel.txt

This revealed two text files in the directory.

Since `cat` was unavailable, I needed another way to read their contents.

### 6. Read Files Using Bash Input Redirection

I discovered that Bash supports reading file contents through input redirection.

I used:

    echo $(<cadabra.txt)

Output:

    Nothing up my sleeve!

Then I tried:

    echo $(<candaniel.txt)

This failed because I had entered an incorrect filename.

After correcting the filename, I executed:

    echo $(< cadaniel.txt)

Output:

    Yes, I did it! I really did it! I'm a true wizard!

This was a major discovery.

The expression:

    $(< filename)

uses Bash command substitution together with input redirection to read a file's contents without requiring the external `cat` command.

The `echo` command then displays the resulting text.

### 7. Explore the Ala Directory

After exploring `abra`, I returned to the home directory:

    cd

I again used Tab completion to inspect the available directories.

Next, I entered:

    cd ala

I checked the current location:

    pwd

Output:

    /home/ctf-player/ala

I then used Tab completion to inspect the files inside this directory.

The shell displayed:

    kazam.txt
    mode.txt

This revealed two more text files.

### 8. Retrieve the Flag

Since I had already discovered how to read files using Bash input redirection, I applied the same technique to `kazam.txt`.

I executed:

    echo $(< kazam.txt)

The shell returned:

    return 0 academy{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01ng_h3r3_17ec7048}

The flag was successfully retrieved!

## Commands and Techniques Used

| Command / Technique | Purpose |
|---|---|
| `ssh -p` | Connect to the remote challenge server using a specific port. |
| `pwd` | Display the current working directory. |
| `cd` | Change the current directory. |
| `cd` without arguments | Return to the user's home directory. |
| `$PATH` | Display the value of the PATH environment variable. |
| Tab completion | Discover matching directory and file names. |
| `echo` | Display text in the terminal. |
| `$(...)` | Perform command substitution in Bash. |
| `< filename` | Redirect a file's contents to standard input. |
| `$(< filename)` | Read a file's contents using Bash without invoking `cat`. |

## Key Concepts Learned

### 1. Bash Built-in Commands

Bash provides built-in commands that are implemented directly inside the shell.

Examples include:

- `cd`
- `echo`
- `pwd`
- `read`
- `printf`
- `type`

These commands can remain available even when external Linux utilities are removed.

This is important when working with restricted environments.

### 2. Command Substitution

Command substitution allows the output of an expression to be used as part of another command.

The general syntax is:

    $(command)

For example:

    echo $(pwd)

Bash executes `pwd`, captures its output, and passes that output to `echo`.

### 3. Bash File Reading Without Cat

One of the most important techniques in this challenge was:

    echo $(< filename)

Normally, we use:

    cat filename

to display a file.

However, Bash supports the following alternative:

    $(< filename)

This uses input redirection to read the file and command substitution to provide its contents to the surrounding command.

It allowed me to read the challenge files without the external `cat` utility.

**Note:** Command substitution removes trailing newline characters and performs word splitting and pathname expansion on unquoted results. It is useful for simple text files, but it is not a general replacement for `cat`.

### 4. Tab Completion

Tab completion is a shell feature that automatically completes commands, filenames, and directory names.

When multiple matches exist, pressing Tab can display the available options.

In this challenge, it was especially useful because the `ls` command was unavailable.

For example:

    cd

Pressing Tab allowed me to discover directories in the home directory.

Similarly:

    cd cada

Pressing Tab revealed matching filenames beginning with `cada`.

### 5. Restricted Linux Environments

A restricted shell may remove common external utilities while still providing access to shell built-ins.

This challenge demonstrated that understanding the shell itself is just as important as knowing standard Linux commands.

## Lessons Learned

- Not every Linux environment provides the usual commands.
- Bash built-ins can still be useful when external utilities are unavailable.
- `pwd` and `cd` help navigate the filesystem without `ls`.
- Tab completion can reveal filenames and directory structures.
- Bash input redirection can be combined with command substitution to read files without `cat`.
- Understanding shell features is essential when working with restricted environments.
- When a familiar command is unavailable, understanding what it does can help identify alternative techniques.

## Result

Successfully explored the restricted Specialer shell, discovered the available directories using tab completion, and retrieved the flag using Bash input redirection and command substitution.

## Flag

    academy{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01ng_h3r3_17ec7048}