# Collaborative Development

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Jeffery John
- **Platform:** picoCTF
- **Year:** 2024
- **File:** `challenge.zip`
- **Primary Tool:** Git

## What I Learned

- Learned how Git branches allow developers to work on different features independently.
- Learned how to inspect and switch between existing branches.
- Learned how to investigate a Git repository when the main branch does not contain all the required information.
- Learned how multiple developers can contribute separate parts of a project.
- Practiced examining branch-specific changes using Git commands.
- Learned that a Git repository can contain useful information across multiple branches, even when the main branch does not reveal the complete result.
- Improved my understanding of version control and collaborative development workflows.

## Approach

1. **Downloaded the challenge files**

   Downloaded the ZIP archive using `wget`:

       wget https://challenge-files.cylabacademy.net/library/ba168001000b5819945cb083f2a76d572dc83f905647eec6ca166c06a77eba03/challenge.zip

2. **Verified and extracted the archive**

   Checked the file type and extracted the archive:

       file challenge.zip
       unzip challenge.zip

   The extraction created a directory named `drop-in`, containing `flag.py` and a `.git` directory.

3. **Inspected the project files**

   Entered the repository and examined the Python file:

       cd drop-in
       ls
       cat flag.py

   The file only displayed:

       print("Printing the flag...")

   The main file did not contain the complete flag.

4. **Investigated the Git repository**

   Tried commands such as:

       git status
       git log
       git log --oneline
       git log -p

   The repository's branches were important to investigate because the challenge description suggested that different team members were working on separate features.

5. **Handled local changes**

   While experimenting, I changed the file's permissions using `chmod +x` and staged and committed that change.

   Git initially prevented me from switching branches because of the uncommitted change. After committing it, I was able to switch to the existing feature branches.

   **Lesson learned:** It is important to avoid unnecessary changes to a challenge repository. If local modifications are blocking a branch switch, inspect them and either discard or preserve them appropriately before continuing.

6. **Explored the feature branches**

   Switched between the existing branches:

       git checkout feature/part-1
       git checkout feature/part-2
       git checkout feature/part-3

   Inspected the Git history and changes on each branch:

       git log -p

   Each branch contained part of the information needed to solve the challenge.

7. **Combined the information from the branches**

   After investigating all three feature branches, I assembled the flag from their contributions.

8. **Recovered the flag**

   The completed flag was:

       academy{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_e9d85913}

## Commands / Tools Used

- `wget` — downloads the challenge archive.
- `file` — identifies the type of the downloaded file.
- `unzip` — extracts the ZIP archive.
- `ls` — lists files and directories.
- `cat flag.py` — displays the contents of the Python file.
- `git status` — shows the current branch and working-tree changes.
- `git log` — displays commit history.
- `git log --oneline` — displays commit history in a concise format.
- `git log -p` — displays commit history and associated changes.
- `git branch` — lists local branches.
- `git checkout <branch>` — switches to an existing branch.
- `git add .` — stages changes in the current directory.
- `git commit -m "message"` — creates a commit with a message.
- `chmod +x flag.py` — adds executable permission to the file.

## Key Concepts

### 1. Git Branches

A branch is a separate line of development within a Git repository.

Developers can use different branches to work on features independently without immediately changing the main branch.

In this challenge, the repository contained three feature branches:

- `feature/part-1`
- `feature/part-2`
- `feature/part-3`

Investigating these branches revealed the information needed to complete the challenge.

### 2. Collaborative Development

In collaborative software development, different team members can work on separate features simultaneously.

Each person may contribute a different part of a larger project. Git helps track those contributions and provides ways to integrate them.

### 3. Switching Between Branches

The command:

    git checkout feature/part-1

switches the working directory to the specified existing branch.

Alternatively, modern Git supports:

    git switch feature/part-1

Use `git branch` to list local branches before switching between them.

### 4. Git History and Diffs

The command `git log -p` displays commit history along with changes introduced by each commit.

This is useful when investigating how files changed or determining what information was added in earlier versions.

### 5. Working-Tree Changes

Git may prevent switching branches when uncommitted changes could be overwritten.

Before switching branches, inspect the current state:

    git status

For a clean challenge workflow, avoid modifying files unless necessary.

## Result

Successfully explored the repository's three feature branches, investigated their Git histories, and combined the information needed to recover the complete flag.

## Flag

academy{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_e9d85913}