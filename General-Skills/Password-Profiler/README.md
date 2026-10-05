# Password Profiler

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Yahaya Meddy
- **Platform:** picoCTF
- **Year:** 2026

## What I Learned

- Learned how personal information can be used to create targeted password guesses.
- Learned how OSINT information can be used to build a custom password wordlist.
- Learned how to inspect and understand Python code before executing it.
- Learned how SHA-1 hashes can be used to verify whether a password candidate is correct.
- Learned how to use CUPP to generate custom password lists from personal information.
- Practiced using Linux commands such as `wget` and `cat` to download and inspect challenge files.
- Learned how a password-checking script can compare candidate passwords against a known hash.
- Improved my understanding of targeted password attacks and custom wordlists.

## Approach

1. Downloaded all the files provided by the challenge using `wget`.

       wget https://challenge-files.cylabacademy.net/library/eee2a66921bd7ab65c6464f5293a9d15cc01c8631a0dc4c9668db8a2525639fc/userinfo.txt

       wget https://challenge-files.cylabacademy.net/library/eee2a66921bd7ab65c6464f5293a9d15cc01c8631a0dc4c9668db8a2525639fc/hash.txt

       wget https://challenge-files.cylabacademy.net/library/eee2a66921bd7ab65c6464f5293a9d15cc01c8631a0dc4c9668db8a2525639fc/check_password.py

2. Verified that the files were downloaded successfully.

       ls

3. Read the personal information provided in `userinfo.txt`.

       cat userinfo.txt

4. Read the SHA-1 hash stored in `hash.txt`.

       cat hash.txt

5. Read the provided Python script to understand how it checks passwords against the hash.

       cat check_password.py

6. After understanding the files and the password-checking logic, used the challenge hint to identify **CUPP (Common User Passwords Profiler)** as the tool for generating a custom wordlist.

7. Used CUPP to generate a password list based on the personal information contained in `userinfo.txt`.

8. Saved the generated password list in the same directory as the challenge files so that the checking script could access it.

9. Ran the provided Python password-checking script with the generated wordlist.

       python3 check_password.py

10. The script tested the generated password candidates against the provided SHA-1 hash and identified the correct password.

11. Used the matching password to complete the challenge and recover the flag.

## Commands / Tools Used

- `wget` — download the challenge files.
- `ls` — verify downloaded files and list the directory contents.
- `cat` — read the contents of the provided files.
- `python3` — execute the password-checking Python script.
- **CUPP** — generate a custom password wordlist from personal information.
- **SHA-1** — hashing algorithm used by the challenge to verify password candidates.

## Key Concepts

### OSINT and Password Profiling

Personal information can sometimes be used to generate likely password candidates. Attackers can collect publicly available information and use it to create targeted wordlists.

### Custom Wordlists

Instead of using a large generic password list, a custom wordlist can be generated specifically for a target.

CUPP automates this process by taking personal information and generating different combinations that may be used as passwords.

### SHA-1 Hash Matching

The challenge does not provide the password directly. Instead, it provides a SHA-1 hash.

The password-checking process can be represented as:

       Password Candidate
              |
              v
          SHA-1 Hash
              |
              v
       Compare with
       Provided Hash
              |
              v
          Match?
         /      \
       Yes       No
        |         |
     Password   Try Next
     Found      Candidate

### Targeted Password Attack

The overall attack path used in this challenge was:

       Personal Information
              |
              v
            CUPP
              |
              v
       Custom Wordlist
              |
              v
       Password Candidates
              |
              v
       SHA-1 Verification
              |
              v
       Correct Password
              |
              v
             Flag

## Result

Successfully downloaded and analyzed the provided files, understood the password-checking script, generated a custom wordlist using CUPP, and used the wordlist to identify the password matching the provided SHA-1 hash.

## Flag

academy{aliceaj7515}