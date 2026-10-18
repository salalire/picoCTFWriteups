# binhexa

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Nana Ama Atombo-Sackey
- **Platform:** picoCTF
- **Year:** 2024
- **Connection:** Netcat
- **Host:** `chatelaine.cylabacademy.net`
- **Port:** `31487`

## What I Learned

- Learned how to perform basic binary arithmetic and bitwise operations.
- Learned the differences between bitwise AND (`&`), OR (`|`), left shift (`<<`), and right shift (`>>`).
- Practiced multiplying and adding binary numbers.
- Learned how to convert binary results into hexadecimal.
- Practiced solving interactive questions through a Netcat connection.
- Learned that binary operations require careful attention to the order of operations and the numbers specified in each question.
- Understood that the final result must be converted to hexadecimal to retrieve the flag.

## Approach

1. **Connected to the challenge server**

   Used Netcat to connect to the challenge:

       nc chatelaine.cylabacademy.net 31487

2. **Read the challenge instructions**

   The server explained that I needed to perform six binary operations in the order provided and then enter the final result in hexadecimal.

3. **Performed the bitwise AND operation**

   The first binary numbers were:

       Binary Number 1: 00110100
       Binary Number 2: 01111000

   The operation was `&`.

   Bitwise AND produces `1` only when both corresponding bits are `1`.

       00110100
       01111000
       --------
       00110000

   Submitted:

       00110000

   The server accepted the answer.

4. **Performed the left shift operation**

   The next operation was `<<`, shifting Binary Number 1 one position to the left.

   Submitted:

       01101000

   The server accepted the answer.

5. **Performed the bitwise OR operation**

   The operation was `|`.

   Bitwise OR produces `1` when at least one of the corresponding bits is `1`.

   Submitted:

       01111100

   The server accepted the answer.

6. **Performed the multiplication operation**

   The operation was `*`, requiring the multiplication of Binary Number 1 and Binary Number 2.

   After correcting my initial attempts, the accepted result was:

       01100001100000

7. **Performed the right shift operation**

   The operation was `>>`, shifting Binary Number 2 to the right by one bit.

   After a few incorrect attempts, the server accepted:

       00111100

8. **Performed the addition operation**

   The final operation was `+`, requiring the addition of the two binary numbers.

   Submitted:

       010101100

   The server accepted the result.

9. **Converted the final result into hexadecimal**

   The server requested the final result in hexadecimal.

   Submitted:

       AC

   The server confirmed the answer and displayed the flag.

## Commands / Tools Used

- `nc chatelaine.cylabacademy.net 31487` — connects to the remote challenge service.
- **Binary arithmetic** — performs addition and multiplication using binary numbers.
- **Bitwise AND (`&`)** — produces `1` only when both corresponding bits are `1`.
- **Bitwise OR (`|`)** — produces `1` when either or both corresponding bits are `1`.
- **Left shift (`<<`)** — shifts bits to the left.
- **Right shift (`>>`)** — shifts bits to the right.
- **Hexadecimal conversion** — converts the final numerical result into base 16.

## Key Concepts

### 1. Binary Numbers

Binary is a base-2 number system that uses only `0` and `1`.

For example:

    Binary:     00110100
    Decimal:    52

Each bit represents a power of two.

### 2. Bitwise AND (`&`)

The AND operation compares corresponding bits and returns `1` only if both bits are `1`.

Example:

    00110100
    01111000
    --------
    00110000

### 3. Bitwise OR (`|`)

The OR operation returns `1` if at least one of the corresponding bits is `1`.

Example:

    00110100
    01111000
    --------
    01111100

### 4. Left Shift (`<<`)

A left shift moves the bits to the left by the specified number of positions.

For example:

    00110100 << 1 = 01101000

For unsigned binary values, shifting left by one position is equivalent to multiplying by two, provided the result is not restricted by a fixed bit width.

### 5. Right Shift (`>>`)

A right shift moves the bits to the right.

For example:

    01111000 >> 1 = 00111100

For unsigned binary values, shifting right by one position is equivalent to integer division by two.

### 6. Binary Multiplication and Addition

Binary arithmetic follows the same general principles as decimal arithmetic, but uses only two digits.

For multiplication, multiply the binary values numerically and convert the result back into binary.

For addition, add the binary values and carry when a column totals two or more.

### 7. Binary-to-Hexadecimal Conversion

Hexadecimal uses sixteen symbols:

    0 1 2 3 4 5 6 7 8 9 A B C D E F

To convert binary to hexadecimal, group the bits into sets of four, starting from the right.

For the final result:

    Binary:      10101100
    Grouped:     1010 1100
    Hexadecimal:    A    C

Therefore:

    10101100 = AC

## Result

Successfully completed all six binary-operation questions, converted the final result to hexadecimal, and recovered the flag.

## Flag

academy{b1tw^3se_0p3eR@tI0n_su33essFuL_e453a847}