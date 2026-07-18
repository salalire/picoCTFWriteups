# Nice netcat...

## Challenge

Connect to a remote server using Netcat, understand the output, and decode it to obtain the flag.

---

## My Approach

1. Connected to the remote service using `nc`.
2. Received a sequence of ASCII values from the server.
3. Converted the ASCII values into text using an ASCII converter.
4. Retrieved the flag.

---

## Commands/Tools Used

```bash
nc wily-courier.picoctf.net <PORT>
```

- Netcat (`nc`)
- ASCII Converter

---

## What I Learned

- How to use **Netcat (`nc`)** to connect to a remote host using its IP/hostname and port.
- How to communicate with remote services from the Linux terminal.
- How to decode ASCII values into readable text.

---

## Key Takeaway

Netcat is a powerful networking tool commonly used in CTFs to interact with remote services, while understanding ASCII encoding is essential for interpreting encoded data.
## Flag 
picoCTF{g00d_k1tty!_n1c3_k1tty!_d5d88}