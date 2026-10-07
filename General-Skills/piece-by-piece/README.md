# Piece by Piece

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Yahaya Meddy
- **Platform:** picoCTF
- **Year:** 2026
- **SSH Host:** xebec.cylabacademy.net
- **SSH Port:** 29239
- **Username:** `ctf-player`

## What I Learned

- Learned how files can be split into multiple parts and later reconstructed.
- Learned how to combine multiple files using `cat`.
- Learned how to identify the purpose of instructions provided inside a challenge environment.
- Practiced working with password-protected ZIP archives.
- Learned how `unzip` can be used to extract password-protected archives.
- Learned the difference between combining file parts and extracting the resulting archive.
- Improved my Linux command-line skills through SSH and file manipulation.
- Learned how binary files can produce unreadable output when viewed directly with `cat`.

## Approach

1. Connected to the remote challenge server using SSH.

       ssh -p 29239 ctf-player@xebec.cylabacademy.net

2. Listed the files in the home directory.

       ls

3. Found the following files:

       instructions.txt
       part_aa
       part_ab
       part_ac
       part_ad
       part_ae

4. Read the instructions to understand how the challenge was structured.

       cat instructions.txt

5. The instructions explained that the flag was stored inside a password-protected ZIP archive that had been split into multiple parts.

6. Combined all the file parts in the correct order using `cat`.

       cat part_aa part_ab part_ac part_ad part_ae > file.zip

7. The resulting `file.zip` was the reconstructed ZIP archive.

8. Attempted to read the binary ZIP file directly with `cat`. The output contained unreadable binary characters, confirming that the file should be treated as an archive rather than normal text.

9. Used `unzip` to extract the reconstructed archive.

       unzip file.zip

10. The archive requested a password. Used the password provided in the challenge instructions:

       supersecret

11. The archive successfully extracted `flag.txt`.

12. Read the extracted file to obtain the flag.

       cat flag.txt

13. The flag was successfully recovered.

## Commands / Tools Used

- `ssh` — connect to the remote challenge environment.
- `ls` — list files in the current directory.
- `cat` — read text files and combine the split file parts.
- `unzip` — extract the reconstructed password-protected ZIP archive.
- `rm` — remove the extracted flag file when testing the extraction process.

## Key Concepts

### Splitting and Combining Files

The original ZIP archive was divided into several parts:

       part_aa
       part_ab
       part_ac
       part_ad
       part_ae

The parts were combined in their correct order using:

       cat part_aa part_ab part_ac part_ad part_ae > file.zip

The `>` operator redirected the combined output into a new file.

### Password-Protected ZIP

After reconstructing the archive, `unzip` was used to extract its contents:

       unzip file.zip

The archive required the password:

       supersecret

After entering the password, the archive extracted `flag.txt`.

### Binary Files

A ZIP file is a binary file, so displaying it with `cat` does not produce meaningful text. Instead, archive-specific tools such as `unzip` should be used to inspect and extract its contents.

## Result

Successfully connected to the remote system, combined the five file parts into a single ZIP archive, extracted the password-protected archive using the provided password, and recovered the flag from `flag.txt`.

## Flag

academy{z1p_and_spl1t_f1l3s_4r3_fun_bbe0be9e}