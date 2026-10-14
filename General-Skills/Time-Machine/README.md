# Time Machine

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

- Learned how Git tracks changes to files over time.
- Learned how to inspect a repository's commit history using `git log`.
- Learned that deleting a file does not necessarily remove its contents from earlier commits.
- Learned how commit messages can provide clues about previous work.
- Practiced investigating a Git repository to recover information that is no longer visible in the current version.
- Learned the importance of version control when tracking development history and recovering previous work.

## Approach

1. **Downloaded the challenge files**

   Downloaded `challenge.zip` from the challenge's provided link.

2. **Extracted the archive**

   Extracted the downloaded ZIP file to access the challenge repository.

3. **Read the challenge description and hints**

   The challenge asked what I had last been working on and mentioned a note intended to help me remember.

   The hints suggested that reading files with `cat` would not be enough and directed me to learn about Git version control and commit messages.

4. **Inspected the Git history**

   I recognized that the challenge involved tracking previous changes rather than simply reading the current file.

   Navigated to the extracted Git repository and ran:

       git log

5. **Examined the commit history**

   The Git history showed three important commits:

   - `Delete flag` — the most recent commit.
   - `Add flag` — the previous commit.
   - An earlier commit containing the flag in its commit message.

   This revealed that the flag had been recorded in the repository's history, even though it was no longer visible in the latest version.

6. **Recovered the flag**

   By examining the older commit information displayed by `git log`, I found the flag in the commit message:

       academy{t1m3m@ch1n3_2e6bda7d}

## Commands / Tools Used

- `unzip challenge.zip` — extracts the downloaded challenge archive.
- `git log` — displays the repository's commit history, including commit messages, authors, and timestamps.
- `cat` — reads the contents of a text file; however, reading the current file alone was not sufficient for this challenge.
- **Git** — tracks changes to files and allows previous versions of a project to be inspected.

## Key Concepts

### 1. Git Version Control

Git is a version control system that records changes to a project over time.

It allows developers to review previous work, compare versions, and recover information from earlier commits.

### 2. Git Commit History

The command `git log` displays the sequence of commits in a repository.

Each commit can contain:
- A commit hash that identifies the commit.
- The author's information.
- The date and time of the commit.
- A commit message describing the change.

In this challenge, the commit history provided the information needed to recover the flag.

### 3. Commit Messages

Commit messages describe the purpose of a change. They can also contain useful information about the work performed.

The challenge's commit history included messages such as `Add flag` and `Delete flag`. The earlier commit message contained the flag itself.

### 4. Deleted Files and Git History

Deleting a file in a new commit does not automatically erase it from previous commits.

Unless the history has been rewritten or the relevant data has otherwise been removed, earlier commits can preserve previous file contents and other recorded information.

### 5. Investigating Git Repositories

When a challenge mentions previous work, deleted files, or forgotten information, inspecting the repository history can reveal clues that are missing from the current working directory.

Useful commands include:

    git log
    git log --oneline
    git show <commit-hash>

The `git show` command can display the details and changes associated with a particular commit.

## Result

Successfully inspected the Git commit history, identified the earlier commit containing the flag, and recovered the hidden information without relying on the current version of the files.

## Flag

academy{t1m3m@ch1n3_2e6bda7d}