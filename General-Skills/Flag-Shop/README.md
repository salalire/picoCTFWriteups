# flag_shop

## Category
General Skills

## Difficulty
Medium

## Challenge Information
- **Platform:** picoCTF
- **Competition:** picoCTF 2019
- **Author:** Danny

## Overview

The challenge presents a flag exchange application where users can check their account balance and purchase different types of flags.

The objective is to purchase the expensive `1337 Flag`, which costs $100,000, despite having insufficient funds initially.

The vulnerability lies in how the application calculates the total purchase cost. By exploiting an **integer overflow**, it is possible to manipulate the account balance and obtain enough money to purchase the actual flag.

## Approach

### 1. Connect to the Flag Shop

I started by connecting to the remote challenge server using Netcat:

    nc chatelaine.cylabacademy.net 44695

The application displayed the following menu:

    Welcome to the flag exchange
    We sell flags

    1. Check Account Balance
    2. Buy Flags
    3. Exit

This provided three options for interacting with the application.

### 2. Inspect the Available Flags

I selected option `2` to purchase flags.

    2

The application displayed two products:

    Currently for sale
    1. Definitely not the flag Flag
    2. 1337 Flag

The first flag was available for $900 each, while the second flag cost $100,000 and had only one available.

Since the objective was to obtain the expensive flag, I needed to increase my account balance.

### 3. Exploit the Integer Overflow

I selected the first option:

    1

The application requested the desired quantity:

    These knockoff Flags cost 900 each, enter desired quantity

Instead of entering a normal quantity, I supplied:

    2500000

The application calculated the final cost as:

    The final cost is: -2044967296

It then displayed my updated account balance:

    Your current balance after transaction: 2044968396

This unexpected result revealed the vulnerability.

#### Understanding Integer Overflow

An integer overflow occurs when an arithmetic operation produces a value outside the range that a variable can represent.

In a typical 32-bit signed integer representation, the maximum positive value is:

    2,147,483,647

The application calculates the purchase cost using:

    Total Cost = Price × Quantity

In this case:

    900 × 2,500,000 = 2,250,000,000

However, `2,250,000,000` exceeds the maximum value of a 32-bit signed integer.

The result wraps around and becomes:

    -2,044,967,296

Instead of deducting money from my account, the application effectively added money because the calculated purchase cost was negative.

The resulting account balance was:

    2,044,968,396

This is the integer overflow vulnerability that made the challenge exploitable.

### 4. Purchase the Actual Flag

After increasing my account balance, I selected option `2` again:

    2

I chose the expensive flag:

    2

The application displayed:

    1337 flags cost 100000 dollars, and we only have 1 in stock
    Enter 1 to buy one

I entered:

    1

Since my manipulated account balance was greater than $100,000, the purchase succeeded.

The application returned:

    YOUR FLAG IS: academy{m0n3y_bag5_A25Fa481}

## Commands and Tools Used

| Command / Tool | Purpose |
|---|---|
| `nc` | Establish a connection to the remote flag shop service. |
| `nc chatelaine.cylabacademy.net 44695` | Connect to the challenge server. |

## Key Concepts Learned

### 1. Integer Overflow

Integer overflow happens when an arithmetic calculation exceeds the maximum or minimum value representable by an integer data type.

In this challenge, multiplying the flag price by a very large quantity caused the calculated cost to exceed the signed 32-bit integer limit.

### 2. Signed 32-bit Integers

A signed 32-bit integer can represent values in this range:

    -2,147,483,648 to 2,147,483,647

The overflow changed the expected positive purchase cost into a negative value.

### 3. Input Validation

Applications should validate user-supplied quantities before performing financial calculations.

Accepting extremely large quantities without checking the resulting arithmetic can introduce vulnerabilities.

### 4. Business Logic Vulnerabilities

Not every security vulnerability involves bypassing authentication or exploiting memory corruption.

Sometimes, incorrect application logic can allow users to manipulate financial calculations and obtain benefits they should not have.

## Lessons Learned

- Always consider the maximum and minimum values supported by integer data types.
- User-controlled input must be validated before being used in financial calculations.
- Never assume that arithmetic operations will always produce the expected result.
- Financial calculations should use safe numeric representations and explicitly check for overflow.
- Understanding the application's source code can reveal weaknesses that are not immediately obvious from its interface.

## Result

Successfully exploited an integer overflow vulnerability in the flag shop's purchase calculation.

By purchasing an extremely large quantity of the cheaper flags, I caused the calculated cost to become negative, increasing my account balance and allowing me to purchase the expensive `1337 Flag`.

## Flag

    academy{m0n3y_bag5_A25Fa481}