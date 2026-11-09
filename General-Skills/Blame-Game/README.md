# Blame Game

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Jeffery John
- **Platform:** picoCTF
- **Year:** 2024
- **Challenge Name:** Blame Game
- **Challenge File:** `challenge.zip`
- **Working Directory:** `~/sald`

## What I Learned

- How to inspect Git commit history to investigate code changes.
- How to identify who made a particular change in a repository.
- How to use `git log` and `git log -p` to investigate previous commits.
- How to use `git blame` to identify the author of changes to individual lines in a file.
- How version control helps developers track changes and troubleshoot problems.

## Approach

### 1. Inspect the Challenge File

I started by navigating to my working directory and listing its contents.

    cd ~/sald
    ls

The directory contained `challenge.zip`. I checked its file type:

    file challenge.zip

The output confirmed that it was a ZIP archive.

### 2. Extract the Challenge Files

I extracted the archive using `unzip`.

    unzip challenge.zip

The archive contained a directory named `drop-in`, which included a Python file called `message.py` and a Git repository in the `.git` directory.

I initially tried `uzip`, but the command was not found. I corrected the command to `unzip`.

### 3. Enter the Repository

I navigated into the extracted directory:

    cd drop-in

I checked the repository's commit history:

    git log
    git log --oneline

These commands help inspect the repository's history and identify the commits that changed the project.

### 4. Investigate Changes to the File

The challenge asked who was responsible for commits that prevented the program from working.

The important step was to investigate the history of `message.py` and identify the author of the suspicious change.

I could inspect the changes introduced by individual commits using:

    git log -p -- message.py

The `-p` option displays patches showing what each commit changed. The `-- message.py` portion limits the history to changes involving that file.

I could also use:

    git blame message.py

This command identifies the commit and author associated with each line of the file. By inspecting the relevant lines and their commit details, I could investigate who introduced the problematic change.

### 5. Identify the Responsible Contributor

I compared the file's changes with the commit history to identify the suspicious modification and its author.

The key was not simply to look at the latest commit, but to inspect the actual changes and determine which contributor introduced the problem.

## Commands / Tools Used

- `ls` — listed files and directories.
- `file challenge.zip` — identified the downloaded file type.
- `unzip challenge.zip` — extracted the challenge archive.
- `cd drop-in` — entered the extracted repository.
- `git log` — displayed detailed commit history.
- `git log --oneline` — displayed a compact commit history.
- `git log -p -- message.py` — displayed patches for changes to `message.py`.
- `git blame message.py` — identified the commits and authors associated with individual lines.

## Key Concepts

### Git Commit History

Git records changes in commits. Each commit includes information such as its author, timestamp, message, and changes.

Examining this history helps developers understand how a project evolved and investigate when a problem was introduced.

### Git Log

The `git log` command displays commit history.

The `--oneline` option provides a compact summary, while `-p` displays the changes introduced by commits.

### Git Blame

The `git blame` command associates each line of a file with the commit and author responsible for that line.

It is useful for investigating suspicious changes, understanding code history, and identifying where a bug may have been introduced.

However, the author of a line is not automatically responsible for a bug; the surrounding changes and commit context should also be examined.

### Troubleshooting with Version Control

When a program stops working, the Git history can help developers trace the changes that may have introduced the problem. Reviewing the actual code differences provides more useful evidence than relying on commit messages alone.

## Lessons Learned

- A Git repository contains useful historical information beyond the current version of its files.
- `git log` helps identify commits, while `git log -p` helps inspect the changes made in those commits.
- `git blame` is especially useful when the task is to determine who introduced a particular line.
- The best way to investigate a suspected bug is to examine both the code changes and the associated commit information.
- Git history is an important tool for debugging and collaboration.

## Result

The challenge focuses on using Git history and line-level attribution to investigate who introduced a problematic change.

## Flag
academy{@sk_th3_1nt3rn_5e805225}