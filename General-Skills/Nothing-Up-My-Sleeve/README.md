# Nothing Up My Sleeve

## Category
General Skills

## Difficulty
Medium

## Challenge Information
- **Platform:** picoCTF
- **Competition:** picoCTF 2020 Mini-Competition
- **Author:** Q0h313th

## Overview

The challenge provides a downloadable file named `flag.txt` and gives a simple hint:

> Let's check that your internet connection is working. This flag is 'in-the-clear', I promise!

The objective was to download the provided file, inspect its contents, and retrieve the flag.

This challenge reinforces basic Linux file-handling commands and downloading files from a remote server using `wget`.

## Approach

### 1. Navigate to the Working Directory

I started by navigating to my challenge directory:

    cd sald/

Then, I listed its contents:

    ls

The directory already contained a file named `flag.txt`.

### 2. Identify the File Type

I used the `file` command to inspect the file:

    file flag.txt

Output:

    flag.txt: ASCII text, with no line terminators

This confirmed that the file contained plain ASCII text rather than a binary or executable file.

### 3. Read the File

I displayed its contents using:

    cat flag.txt

Output:

    academy{c0ngr4ts_0n_y0ur_s4n1ty}

The flag was already present in the file.

### 4. Remove and Download the Challenge File Again

To practice downloading the challenge file from the provided URL, I removed the existing text file:

    rm **.txt

Then I confirmed that the directory was empty:

    ls

Next, I downloaded the original challenge file using `wget`:

    wget https://challenge-files.cylabacademy.net/library/f03ad2ed8692215b1286b3906a5027182df819365a811ef9b48a4d20841e441d/flag.txt

The download completed successfully:

    HTTP request sent, awaiting response... 200 OK
    Length: 32 [application/octet-stream]
    Saving to: 'flag.txt'

    flag.txt 100%[===================>] 32

### 5. Verify the Downloaded File

I listed the directory again:

    ls

Output:

    flag.txt

I checked the file type:

    file flag.txt

Output:

    flag.txt: ASCII text, with no line terminators

Finally, I displayed the downloaded file:

    cat flag.txt

Output:

    academy{c0ngr4ts_0n_y0ur_s4n1ty}

The flag was successfully retrieved.

## Commands and Tools Used

| Command | Purpose |
|---|---|
| `cd sald/` | Navigate to the challenge working directory. |
| `ls` | List files and directories. |
| `file flag.txt` | Identify the file type. |
| `cat flag.txt` | Display the file contents. |
| `rm **.txt` | Remove matching text files in the current directory. |
| `wget <URL>` | Download a file from a remote server. |

## Key Concepts Learned

### 1. Plaintext Files

A plaintext file stores readable characters rather than encoded or compiled binary data. The `file` command helps identify the type of a file.

### 2. Downloading Files with wget

`wget` is a command-line utility for retrieving files from web servers.

Basic syntax:

    wget <URL>

In this challenge, the server returned HTTP status `200 OK`, indicating that the download request was successful.

### 3. Understanding HTTP 200 OK

HTTP status code `200 OK` indicates that the server successfully processed the request and returned the requested resource.

### 4. Reading Files in Linux

The `cat` command displays file contents directly in the terminal. It is particularly useful when inspecting small text files.

## Lessons Learned

- Not every cybersecurity challenge requires complex exploitation or encoding techniques.
- Always inspect the files provided by a challenge before assuming additional steps are necessary.
- The `file` command helps determine whether a file contains readable text or another type of data.
- `wget` is a useful Linux utility for downloading resources directly from the terminal.
- Pay attention to challenge descriptions: sometimes the hint tells you exactly what to look for.

## Result

Successfully downloaded and inspected the provided `flag.txt` file and retrieved the flag.

## Flag

    academy{c0ngr4ts_0n_y0ur_s4n1ty}