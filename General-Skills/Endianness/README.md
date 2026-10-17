# Endianness

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
- **Port:** `34627`
- **Source File:** `flag.c`

## What I Learned

- Learned the difference between little-endian and big-endian representations.
- Learned how to convert ASCII characters into hexadecimal values.
- Practiced using CyberChef to convert text into hexadecimal.
- Learned how byte order affects the representation of a word.
- Practiced interacting with a remote CTF service using Netcat.
- Learned that the same word can have different byte orders depending on the endianness.
- Understood why it is important to distinguish between hexadecimal representations and decimal byte values.

## Approach

1. **Connected to the challenge server**

   Used Netcat to connect to the remote service:

       nc chatelaine.cylabacademy.net 34627

2. **Read the challenge instructions**

   The server explained that I needed to provide both the little-endian and big-endian representations of a given word.

   The word provided was:

       xflyh

3. **Converted the word into hexadecimal**

   Used CyberChef to convert the word into its hexadecimal representation.

   The ASCII characters corresponded to these hexadecimal byte values:

   - `x` → `78`
   - `f` → `66`
   - `l` → `6c`
   - `y` → `79`
   - `h` → `68`

   Therefore, the hexadecimal representation in the original character order was:

       78666c7968

4. **Found the little-endian representation**

   Little-endian stores the least significant byte first. For this challenge, the order of the bytes was reversed:

       68 79 6c 66 78

   The server expected the hexadecimal byte values represented as decimal numbers joined together.

   Converting each byte from hexadecimal to decimal gave:

   - `68` (hex) → `104` (decimal)
   - `79` (hex) → `121` (decimal)
   - `6c` (hex) → `108` (decimal)
   - `66` (hex) → `102` (decimal)
   - `78` (hex) → `120` (decimal)

   Combining the decimal values produced:

       104121108102120

   My first attempt was rejected, so I rechecked the expected format. The correct little-endian answer was:

       68796c6678

   The server accepted this representation.

5. **Found the big-endian representation**

   Big-endian keeps the bytes in their original order.

   The hexadecimal representation was:

       78666c7968

   I entered this value, and the server accepted it.

6. **Retrieved the flag**

   After both representations were accepted, the server displayed the flag.

## Commands / Tools Used

- `nc chatelaine.cylabacademy.net 34627` — connects to the remote challenge service.
- **CyberChef** — converts the word into hexadecimal representation.
- **ASCII table** — helps identify the hexadecimal values corresponding to characters.
- **Hexadecimal conversion** — represents each character's byte value using two hexadecimal digits.

## Key Concepts

### 1. What Is Endianness?

Endianness describes the order in which bytes are arranged when representing multi-byte data.

The two common types are:

- **Little-endian:** Stores the least significant byte first.
- **Big-endian:** Stores the most significant byte first.

### 2. ASCII and Hexadecimal

ASCII assigns numeric values to characters. Hexadecimal is a convenient way to represent those values.

For the word `xflyh`:

    x  f  l  y  h
    78 66 6c 79 68

The complete hexadecimal representation is:

    78666c7968

### 3. Little-Endian Representation

Reversing the order of the bytes gives:

    Original:    78 66 6c 79 68
    Little-endian: 68 79 6c 66 78

The answer expected by this challenge was:

    68796c6678

### 4. Big-Endian Representation

Big-endian preserves the original byte order:

    78 66 6c 79 68

The answer expected by this challenge was:

    78666c7968

### 5. Important Lesson About Byte Order

Reverse the **bytes**, not the individual hexadecimal digits within each byte.

For example:

    Original: 78 66 6c 79 68
    Reversed: 68 79 6c 66 78

Do not reverse the entire hexadecimal string character by character, because that would change the individual byte values.

Also, this challenge expected hexadecimal representations, not the concatenated decimal byte values attempted initially.

## Result

Successfully converted the word `xflyh` into hexadecimal, identified the correct little-endian and big-endian representations, and received the flag.

## Flag

academy{3ndi4n_sw4p_su33ess_66f9bdaa}