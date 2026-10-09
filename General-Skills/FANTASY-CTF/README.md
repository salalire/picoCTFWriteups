# FANTASY CTF

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** syreal
- **Platform:** picoCTF
- **Year:** 2025
- **Connection:** Netcat
- **Host:** `chatelaine.cylabacademy.net`
- **Port:** `19360`

## What I Learned

- Learned how to connect to a remote challenge using Netcat.
- Learned how interactive terminal applications communicate with users through text and input prompts.
- Practiced following instructions and selecting options in an interactive game.
- Learned about important picoCTF competition rules, including avoiding multiple accounts and account sharing.
- Learned why CTF participants should keep flags and challenge artifacts private.
- Learned the importance of ethical behavior and responsible use of cybersecurity skills.
- Practiced navigating a challenge by reading its output and responding to the prompts.
- Learned that some General Skills challenges focus on understanding terminal interaction and competition guidelines rather than exploiting vulnerabilities.

## Approach

1. Connected to the remote challenge using Netcat.

       nc chatelaine.cylabacademy.net 19360

2. Read the introductory story and followed the instructions displayed by the interactive program.

3. Pressed Enter whenever the program prompted me to continue.

4. When the registration options appeared, selected option `c` to register a single, private account.

       [a/b/c] > c

5. Continued through the introductory message, which explained the purpose of picoCTF and emphasized using cybersecurity knowledge responsibly.

6. Followed the instructions to begin the introductory sanity challenge.

7. When presented with the game options, selected option `a` to play the game rather than searching the Ether for the flag.

       [a/b] > a

8. Waited for the simulation to complete successfully.

9. Continued through the remaining prompts until the program displayed the flag.

10. Recorded the flag provided by the challenge.

## Commands / Tools Used

- `nc` — establish a connection to the remote interactive challenge.
- `Enter` — advance through the story and continue past prompts.
- Interactive menu selection — choose the appropriate options by entering the corresponding letter.

## Key Concepts

### Netcat

Netcat (`nc`) is a command-line utility used to establish network connections and communicate with services over TCP or UDP.

In this challenge, Netcat provided access to the interactive Fantasy CTF simulation.

### Interactive Terminal Applications

Some terminal programs present users with menus, questions, and instructions. To complete these challenges, read the displayed information carefully and enter the requested response.

For example:

       Options:
       A) Register multiple accounts
       B) Share an account with a friend
       C) Register a single, private account

The challenge expected the user to enter the corresponding letter and press Enter.

### picoCTF Competition Rules

The simulation highlighted several important competition guidelines:

- Register only one account.
- Do not share an account with another participant.
- Do not share flags or challenge artifacts.
- Wait until the winners have been announced before publishing challenge writeups.
- Use cybersecurity skills responsibly and ethically.

### Responsible Cybersecurity

Cybersecurity knowledge should be used to protect systems, investigate vulnerabilities responsibly, and defend against malicious activity.

The challenge reinforces the importance of ethical conduct while participating in cybersecurity competitions.

## Result

Successfully connected to the Fantasy CTF simulation, followed the interactive prompts, completed the introductory game, and recovered the flag.

## Flag

academy{m1113n1um_3d1710n_401821da}