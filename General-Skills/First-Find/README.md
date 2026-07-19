# First Find

## Challenge
The challenge provides a ZIP archive containing many directories and files. The objective is to locate a file named `uber-secret.txt` and read its contents to obtain the flag.

## What I Learned
- How to extract ZIP archives using `unzip`.
- How hidden directories (`.`) work in Linux.
- Why manually browsing directories is inefficient.
- How to use the `find` command to quickly locate files in large directory structures.
- The difference between `find` (searching for files) and `grep` (searching inside files).

## Tools Used
- `file`
- `unzip`
- `find`
- `cat`

## Flag
picoCTF{f1nd_15_f457_ab443fd1}

## Commands Used

```bash
file files.zip
unzip files.zip
find . -name "uber-secret.txt"
cat ./adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
