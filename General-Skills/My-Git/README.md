# My Git

## Category

General Skills

## Difficulty

Easy

## What I Learned

- Learned that Git stores the author's name and email address inside each commit.
- Learned that `git config user.name` and `git config user.email` can be configured on a repository-specific basis.
- Learned that Git does not automatically verify whether the identity in a commit actually belongs to the person making the commit.
- Learned how commit metadata can be used to impersonate another Git user.
- Practiced cloning a Git repository over SSH and pushing changes to a remote server.
- Learned how a custom Git server can inspect commit metadata and files before accepting a push.

## Approach

1. Cloned the challenge repository using the provided SSH Git URL.

2. Entered the cloned repository and configured a repository-specific Git identity:
   
       git config user.name "root"
       git config user.email "root@academy"

3. Created a file named `flag.txt` containing the required text:

       echo "give me flag" > flag.txt

4. Added the file to the Git staging area:

       git add .

5. Created a commit using the impersonated `root` identity:

       git commit -m "add"

6. Pushed the commit to the remote Git server:

       git push

7. The server inspected the commit and detected that:
   - The commit author matched the `root` user.
   - `flag.txt` was included in the commit.

8. The server accepted the push and returned the flag.

## Commands / Tools Used

- Git
- SSH
- `git clone`
- `git config`
- `git add`
- `git commit`
- `git push`
- Git commit metadata

## Key Concept

Git commits contain author information such as:

    Author: Name <email>

This information is normally configured with:

    git config user.name "Name"
    git config user.email "email"

For a single repository, these settings can be changed without affecting the global Git configuration.

In this challenge, the server trusted the identity stored in the commit metadata. By configuring the repository to use the `root` identity and creating a commit, the challenge server recognized the commit as being authored by `root`.

The important lesson is that **Git's local author information is metadata and should not be treated as proof of a user's real identity by itself.**

## Result

The remote Git server verified the commit author and detected `flag.txt`, then returned the challenge flag.

## Flag

academy{1mp3rs0n4t4_g17_345y_7d9222cd}