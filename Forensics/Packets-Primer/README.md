# picoCTF 2022 - Packets Primer Writeup

## Challenge Information

- **Challenge:** Packets Primer
- **Category:** Forensics
- **Difficulty:** Medium
- **Platform:** picoCTF 2022

## Description
Download the packet capture file and use packet analysis software to find the flag.

Download packet capture

The objective is to analyze the packets and recover the hidden flag using packet analysis software.

---

## Challenge I Faced

This was my first challenge involving packet capture (PCAP) analysis.

Initially, I did not know where to begin because a packet capture contains many different protocols and packet fields.

I first identified the file type and then opened it with **Wireshark** to inspect the captured network traffic.

---

## My Approach

### 1. Identify the file type

First, I verified the type of the downloaded file.

```bash
file network-dump.flag.pcap
```

Output:

```
network-dump.flag.pcap:
pcap capture file, microsecond ts (little-endian)
version 2.4 (Ethernet, capture length 262144)
```

This confirmed that the file was a valid **PCAP network capture**.

---

### 2. Open the capture in Wireshark

I opened the capture using Wireshark.

```bash
wireshark network-dump.flag.pcap
```

---

### 3. Inspect the packets

After opening the capture, I examined each packet.

For every packet, Wireshark displays:

- Ethernet Header
- IPv4 Header
- TCP Header
- Packet Data (Payload)

The flag was stored inside the **TCP Data** section.

---

### 4. View the packet payload

After selecting the correct packet, I expanded:

```
Transmission Control Protocol
    └── Data
```

The payload appeared in both **Hex** and **ASCII** formats.

The ASCII representation clearly showed the flag:

```
picoCTF{p4ck37_5h4rk_ceccaa7f}
```

---

## What I Learned

- A **PCAP** file stores captured network traffic.
- The `file` command identifies packet capture files before analysis.
- **Wireshark** is one of the most important tools for network forensics.
- Every packet consists of multiple protocol layers, such as:
  - Ethernet
  - IP
  - TCP/UDP
  - Application Data
- The **Data (Payload)** section often contains the actual transmitted information.
- Wireshark displays packet payloads in both **Hexadecimal** and **ASCII**, making it easy to recognize readable text such as flags.
- Not every challenge requires complicated filters—sometimes simply inspecting the packet payload is enough.

---

## Flag

```text
picoCTF{p4ck37_5h4rk_ceccaa7f}
```