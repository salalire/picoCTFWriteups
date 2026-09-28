# ping-cmd

## Category

General Skills

## Difficulty

Easy

## What I Learned

- Learned how user-supplied input can be passed to system commands.
- Learned how command injection vulnerabilities can occur when input is not properly validated or sanitized.
- Learned how shell metacharacters can alter the intended execution flow of a command.
- Practiced identifying command injection opportunities in a web-based command interface.
- Learned how to use command chaining to make a server execute additional commands.
- Improved my understanding of how applications interact with operating-system commands.

## Approach

1. Opened the challenge and identified a web interface that accepts an address to ping.
2. Tested the normal functionality by providing a valid host such as Google's DNS server.
3. Observed that the application appeared to execute the supplied input through a system command.
4. Considered whether additional shell commands could be appended to the expected ping input.
5. Tested shell command injection using command separators to determine whether the server would execute additional commands.
6. Used the resulting command execution to inspect the server and locate the hidden information.
7. Retrieved the flag from the server.

## Commands / Techniques Used

- Web browser
- Ping
- Shell command injection
- Command chaining
- Linux command-line utilities

## Key Concept

The vulnerability occurs when an application directly incorporates user-controlled input into a system command without properly validating or escaping it.

For example, an application may intend to execute:

    ping <user_input>

If the input is not safely handled, shell operators can potentially cause additional commands to be executed instead of treating the entire input as a hostname.

## Flag
academy{p1nG_c0mm@nd_3xpL0it_su33essFuL_7c0b936f}
