# ABSOLUTE NANO

## Category

General Skills

## Difficulty

Medium

## Challenge Information

- **Author:** Darkraicg492
- **Platform:** picoCTF
- **Year:** 2026
- **Challenge Name:** ABSOLUTE NANO
- **Target Host:** `xebec.cylabacademy.net`
- **SSH Port:** `31657`
- **User:** `ctf-player`

## What I Learned

- How to connect to a remote Linux machine using SSH.
- How to inspect sudo privileges using `sudo -l`.
- How to identify security risks caused by misconfigured sudo permissions.
- How to use the GNU nano text editor.
- How an editor running with root privileges can potentially provide access to files that an ordinary user cannot read.
- How Linux file permissions and privilege escalation relate to one another.

## Approach

### 1. Connect to the Remote Machine

I connected to the challenge server using SSH.

    ssh -p 31657 ctf-player@xebec.cylabacademy.net

When prompted, I entered the provided password:

    42e0946c

SSH established a remote terminal session on the challenge machine.

### 2. Inspect the Home Directory

After logging in, I listed the files in the current directory.

    ls

The output showed:

    flag.txt

Although the file existed, the challenge focused on understanding how to access files when ordinary user permissions restrict access.

### 3. Check Sudo Permissions

I ran:

    sudo -l

The output showed that `ctf-player` could execute the following command without entering a password:

    (ALL) NOPASSWD: /bin/nano /etc/sudoers

This was the key finding.

The permission allowed the user to run the nano editor as another user, including root, for the specified file.

**Why this matters:**

- `sudo` allows authorized commands to run with another user's privileges.
- `NOPASSWD` means sudo does not require a password for the permitted command.
- `/bin/nano` is the path to the nano text editor.
- `/etc/sudoers` is the configuration file that defines sudo permissions.

The important security issue was that nano was permitted to run with elevated privileges.

### 4. Launch Nano with Sudo

I executed:

    sudo /bin/nano /etc/sudoers

This opened `/etc/sudoers` in nano with elevated privileges.

The key lesson was that granting permission to launch a powerful text editor as root can create a privilege-escalation risk. Depending on the editor's capabilities and the restrictions imposed by the environment, an authorized user may be able to access files beyond their normal permissions.

### 5. Understand the Privilege Escalation Concept

Linux restricts access to files according to ownership, permissions, and the privileges of the current process.

For example, an ordinary user might not be allowed to read a file owned by root. However, if the user can launch a sufficiently powerful editor with root privileges, the editor may be able to access that file.

This illustrates why administrators should avoid granting unrestricted access to general-purpose editors through sudo.

**Note:** The supplied terminal transcript shows that nano was launched, but it does not show the final flag output or the exact steps used to retrieve it.

## Commands / Tools Used

- `ssh -p 31657 ctf-player@xebec.cylabacademy.net` — connected to the remote challenge machine.
- `ls` — listed files in the current directory.
- `sudo -l` — displayed the commands the user was authorized to run with sudo.
- `sudo /bin/nano /etc/sudoers` — launched nano with elevated privileges to edit or inspect the sudoers configuration.

## Key Concepts

### Linux File Permissions

Linux uses file ownership and permission rules to control who can read, write, or execute files.

A user who lacks permission to read a file directly may still gain access through a process running with sufficient privileges.

### Sudo Misconfiguration

Sudo can grant permission to execute specific commands as another user.

Allowing a user to run a general-purpose editor with elevated privileges can be dangerous because editors may provide capabilities beyond simply modifying the specified file.

### Nano

Nano is a terminal-based text editor that allows users to create, view, and modify text files.

When launched with elevated privileges, it operates with those privileges. Therefore, the permissions of the editor process can be more important than the permissions the user normally has.

### Privilege Escalation

Privilege escalation occurs when a user gains permissions beyond those originally assigned to them.

In this challenge, the sudo rule was the important potential escalation path because it authorized running nano with elevated privileges.

## Security Lessons Learned

- Always inspect sudo permissions during a Linux privilege-escalation assessment.
- Understand exactly which commands a sudo rule permits.
- Avoid granting unrestricted access to editors or other general-purpose utilities as root.
- Apply the principle of least privilege when configuring sudo.
- Remember that a program launched with elevated privileges can access resources unavailable to its ordinary user.
- Treat sudo configuration as an important part of Linux system security.

## Result

Identified a potentially dangerous sudo permission that allowed the `ctf-player` user to launch nano with elevated privileges.

The central lesson was understanding how a misconfigured sudo rule can potentially allow access to files that the user cannot read directly.

## Flag

academy{n4n0_411_7h3_w4y_81311b87}