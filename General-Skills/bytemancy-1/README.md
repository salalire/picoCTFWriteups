# bytemancy 1

## Category

General Skills

## Difficulty

Easy

## What I Learned

- Learned how ASCII characters can be represented using decimal values.
- Learned how to interpret a server instruction that requires a specific byte value to be repeated.
- Practiced generating large amounts of structured input with Python instead of typing it manually.
- Learned how to send generated input to a remote service using `nc` (Netcat).
- Improved my understanding of how byte-oriented challenges validate exact input.

## Approach

1. Started the challenge instance and connected to the remote service using Netcat.

2. The server displayed the following requirement:

       Send me ASCII DECIMAL 101 1751 times, side-by-side, no space.

3. Interpreted `101` as an ASCII decimal value.

4. Determined that ASCII decimal `101` represents the character:

       e

5. The server required the value `101` to appear exactly `1751` times with no spaces between the values.

6. Instead of manually typing the value thousands of times, used Python to generate the required input automatically:

       python3 -c 'print("101" * 1751)'

7. Sent the generated input to the challenge service through the Netcat connection.

8. The server validated the byte sequence and accepted the correct input.

## Commands / Tools Used

- Netcat (`nc`)
- Python 3
- ASCII
- Decimal byte representation

## Key Concept

ASCII assigns numeric values to characters.

For example:

    Decimal 101 → ASCII character 'e'

However, this challenge does not require sending the character `e`. It specifically asks for the **ASCII decimal representation** `101`.

The important part is also the formatting requirement:

    101101101101...

There must be:

- Exactly `1751` occurrences of `101`
- No spaces
- No additional characters

Python is useful for this because string multiplication can generate the required sequence accurately:

    "101" * 1751

This produces the value `101` repeated exactly 1751 times.

## Result

The required byte sequence was generated programmatically and submitted to the challenge service using Netcat.

## Flag
academy{h0w_m4ny_e's???_6fd2faa9}
