# Printer Shares

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Janice Hepi
- **Platform:** picoCTF
- **Year:** 2026
- **Protocol:** SMB
- **Objective:** Access the public network share on the print server and retrieve the accidentally shared file containing the flag.

## What I Learned

- Learned how the SMB protocol can be used to share files over a network.
- Learned how to check whether a remote TCP port is accessible using `nc`.
- Learned how to use `smbclient` to interact with SMB shares.
- Learned how to enumerate available SMB shares on a remote server.
- Learned how anonymous/guest SMB access can expose publicly accessible files.
- Learned how to connect directly to a specific SMB share.
- Learned how to list files available inside an SMB share.
- Learned how to download a remote file using the `get` command.
- Practiced applying the challenge hints by using `smbclient` to investigate the printer share.

## Approach

1. First checked whether the provided printer port was reachable using Netcat.

       nc -vz chatelaine.cylabacademy.net 17192

2. The connection succeeded, confirming that the target TCP port was accessible.

       Connection to chatelaine.cylabacademy.net (18.227.187.235) 17192 port [tcp/*] succeeded!

3. Initially attempted to enumerate SMB shares without specifying the custom port.

       smbclient -L //18.227.187.235 -N

4. The connection timed out because SMB was running on a non-standard port.

       NT_STATUS_IO_TIMEOUT

5. Used the challenge hint and specified the discovered port with `smbclient`.

       smbclient -L //18.227.187.235 -p 17192 -N

6. The command successfully enumerated the available SMB shares.

       Sharename       Type      Comment
       ---------       ----      -------
       shares          Disk      Public Share With Guests
       IPC$            IPC       IPC Service (Samba 4.19.5-Ubuntu)

7. The `shares` share was identified as a public disk share that allowed guest access.

8. Connected to the `shares` SMB share anonymously using `-N`.

       smbclient //18.227.187.235/shares -p 17192 -N

9. Used the SMB `ls` command to list the files available in the share.

       ls

10. The share contained two files:

       dummy.txt
       flag.txt

11. Tried to use `cat` and `file` inside the `smbclient` prompt, but these are local Linux commands and were not available as SMB commands.

12. Used the SMB `get` command to download `flag.txt` from the remote share.

       get flag.txt

13. Exited the SMB session and verified that the file was downloaded to the local directory.

       exit
       ls

14. Read the downloaded file using the normal Linux `cat` command.

       cat flag.txt

15. The flag was successfully recovered.

## Commands / Tools Used

- `nc` — check whether the remote TCP port is accessible.
- `smbclient` — interact with SMB servers and shares.
- `smbclient -L` — enumerate available SMB shares.
- `-p` — specify the non-standard SMB port.
- `-N` — connect without providing a password.
- `ls` — list files inside the SMB share.
- `get` — download a file from the SMB share.
- `exit` — leave the `smbclient` session.
- `cat` — read the downloaded file locally.

## Key Concepts

### SMB

SMB (Server Message Block) is a network protocol commonly used for sharing files, directories, printers, and other resources over a network.

In this challenge, SMB was being used to expose a public share containing the accidentally shared file.

### SMB Share Enumeration

The following command was used to discover available shares:

       smbclient -L //18.227.187.235 -p 17192 -N

The `-L` option asks the SMB server to list its available shares.

The result showed:

       shares

This was the share we needed to investigate.

### Anonymous / Guest Access

The `-N` option allowed the connection without providing a password.

       smbclient -L //18.227.187.235 -p 17192 -N

This worked because the challenge's SMB share permitted guest access.

### Downloading Files from an SMB Share

After connecting to the share:

       smbclient //18.227.187.235/shares -p 17192 -N

The `ls` command showed the available files. The remote `flag.txt` file was downloaded using:

       get flag.txt

After leaving `smbclient`, the file could be read normally:

       cat flag.txt

## Important Observation

The challenge used a **non-standard SMB port** rather than the default SMB ports. This is why the first attempts without `-p 17192` timed out.

The successful workflow was:

       Check Port
            |
            v
       Enumerate SMB Shares
            |
            v
       Connect to Public Share
            |
            v
       List Files
            |
            v
       Download flag.txt
            |
            v
       Read Flag

## Result

Successfully used SMB enumeration and anonymous access to find the public `shares` directory, downloaded `flag.txt` using `smbclient`, and recovered the flag.

## Flag

academy{5mb_pr1nter_5h4re5_6f6353d3}