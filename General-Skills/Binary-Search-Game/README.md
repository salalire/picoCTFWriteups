# Binary Search Game

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Platform:** picoCTF
- **Challenge Type:** Binary Search / Shell
- **Remote Host:** xebec.cylabacademy.net
- **Objective:** Find a randomly selected number between 1 and 1000 using no more than 10 guesses.

## What I Learned

- Learned how the binary search algorithm works.
- Learned how to efficiently search through a large range by repeatedly dividing it in half.
- Learned how the `Higher!` and `Lower!` responses can be used to eliminate large portions of the search space.
- Practiced using SSH to connect to a remote challenge environment.
- Learned that each new connection generates a new random target number.
- Learned why a new binary search must start from the beginning when reconnecting.
- Improved my ability to calculate the next guess based on the current lower and upper bounds.
- Learned how binary search can reduce 1000 possible values to a small number of guesses.

## Approach

1. Connected to the remote challenge using SSH.

       ssh -p 11578 ctf-player@xebec.cylabacademy.net

2. Entered the provided password when prompted.

3. The program explained that it was thinking of a number between `1` and `1000` and that there were only `10` guesses available.

4. My first attempt did not use a proper binary search. I made several guesses such as `250`, `500`, `750`, `850`, `900`, and `950`, which eventually exceeded the maximum number of guesses.

5. Started a new SSH connection. The challenge generates a new random number for every connection, so the previous search could not be continued.

6. On another attempt, I used binary-search-style guesses. After guessing `500`, the program responded with `Lower!`, meaning the target was between `1` and `499`.

7. Guessed `250` and received `Higher!`, reducing the possible range to approximately `251–499`.

8. Continued narrowing the range using the midpoint of the remaining possibilities.

9. The successful sequence was:

       500 → Higher
       750 → Higher
       875 → Higher
       938 → Lower
       908 → Higher
       923 → Higher
       931 → Lower
       927 → Higher
       929 → Higher
       930 → Correct

10. The program confirmed that `930` was the correct number and displayed the flag.

## Commands / Tools Used

- `ssh` — connect to the remote challenge server.
- `11578` — SSH port used for the successful challenge instance.
- Binary search — algorithm used to efficiently narrow down the possible number.

## Key Concepts

### Binary Search

Binary search works by repeatedly dividing a sorted search range into two parts.

For a range from `1` to `1000`, the first useful guess is around the middle:

       1 ---------------- 500 ---------------- 1000

If the program responds with `Higher!`, the lower half can be eliminated.

If it responds with `Lower!`, the upper half can be eliminated.

The process continues until the correct number is found.

### Example

For the successful attempt:

       Range: 1–1000
       Guess: 500
       Result: Higher

The target must therefore be greater than `500`.

       Range: 501–1000
       Guess: 750
       Result: Higher

Now:

       Range: 751–1000
       Guess: 875
       Result: Higher

Then:

       Range: 876–1000
       Guess: 938
       Result: Lower

The search range continues shrinking until only a small number of possibilities remain.

### Why a New Connection Requires a New Search

The challenge randomly chooses a new number every time a new connection is made.

Therefore, if a connection is closed and a new one is started, the previous target number is no longer relevant. The binary search must start again from the full range of `1–1000`.

## Result

Successfully used binary search to identify the target number `930` within the allowed 10 guesses and recovered the flag.

## Flag

academy{g00d_gu355_1b252bff}