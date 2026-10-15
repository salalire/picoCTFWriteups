# Commitment Issues

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Jeffery John
- **Platform:** picoCTF
- **Year:** 2024
- **Primary Tool:** Git
- **File:** `message.txt`

## What I Learned

- Learned how Git tracks changes to files through commits.
- Learned how to inspect commit history using `git log`.
- Learned how to display a simplified commit history using `git log --oneline`.
- Learned how to examine changes introduced by commits using `git log -p`.
- Learned that deleting sensitive information from the latest version of a file does not necessarily remove it from the Git history.
- Practiced recovering information from previous commits.
- Understood why developers should avoid committing sensitive information to version control.

## Approach

1. **Downloaded and extracted the challenge files**

   Downloaded the challenge files and extracted the archive to access the Git repository.

2. **Examined the challenge description**

   The challenge stated:

       I accidentally wrote the flag down. Good thing I deleted it!

   This suggested that the flag had been deleted from the current version but might still exist in an earlier commit.

3. **Inspected the commit history**

   Ran the following command to view the repository's commit history:

       git log

   The history showed two important commits:
   - `remove sensitive info`
   - `create flag`

   These commit messages suggested that the flag had first been added and then replaced.

4. **Viewed the simplified history**

   Used:

       git log --oneline

   This displayed the commits in a compact format, making it easier to identify the sequence of changes.

5. **Examined the changes in each commit**

   Ran:

       git log -p

   The `-p` option displayed the differences introduced by each commit.

   The latest commit showed that `message.txt` had changed from:

       academy{s@n1t1z3_f1ce74e2}

   to:

       TOP SECRET

   The earlier commit showed that the original file contained the flag.

6. **Recovered the flag**

   By examining the previous version of `message.txt` in the Git history, I recovered the flag that had been removed from the current version.

## Commands / Tools Used

- `git log` — displays the repository's commit history.
- `git log --oneline` — displays a concise summary of commits.
- `git log -p` — displays commit history along with the changes introduced by each commit.
- **Git** — tracks changes to files and preserves committed versions of a project.

## Key Concepts

### 1. Git Version Control

Git is a version control system that records changes to files over time. It allows developers to review previous work and inspect earlier versions of their projects.

### 2. Git Commit History

Each commit records a snapshot of the tracked project and includes information such as its commit hash, author, timestamp, and message.

Even if a file changes or is deleted in a later commit, earlier committed versions may still be accessible through the repository's history.

### 3. Understanding `git log -p`

The `-p` option displays the patches associated with commits.

In a patch:
- Lines beginning with `-` represent content removed by that change.
- Lines beginning with `+` represent content added by that change.

In this challenge, the output revealed the original flag because it appeared on a removed line.

### 4. Deleted Information in Git

Removing information from a file does not automatically erase it from earlier commits.

This means that sensitive information committed accidentally may remain accessible in the repository history even after it has been replaced or deleted.

### 5. Protecting Sensitive Information

Developers should avoid committing passwords, API keys, private credentials, or other sensitive information to Git repositories.

If sensitive information is accidentally committed, deleting it from the latest version is not enough. The secret should be revoked or rotated, and the repository history should be addressed when necessary.

## Result

Successfully inspected the Git commit history, identified the change that replaced the original flag with `TOP SECRET`, and recovered the flag from the earlier commit.

## Flag

academy{s@n1t1z3_f1ce74e2}