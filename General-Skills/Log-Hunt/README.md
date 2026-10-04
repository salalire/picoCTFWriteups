
# Log Hunt

## Category

General Skills

## Difficulty

Easy

## Challenge Information

- **Author:** Yahaya Meddy
- **Platform:** picoCTF
- **Event:** picoMini by CMU-Africa

## What I Learned

- Learned how to analyze server log files to find hidden information.
- Learned how to use `grep` to search for specific text patterns in logs.
- Practiced identifying flag fragments scattered across multiple log entries.
- Learned how to recognize repeated log entries and avoid treating duplicates as separate fragments.
- Improved my Linux command-line skills by filtering log data using different search patterns.
- Learned how sensitive information can accidentally be exposed through server logs.
- Practiced reconstructing a complete flag by combining its fragments in the correct order.

## Approach

1. Navigated to the directory containing the downloaded `server.log` file.

2. Searched for entries containing `aca` to identify the beginning of the flag.

       cat server.log | grep aca

3. Searched for entries containing underscores to discover additional flag fragments.

       cat server.log | grep _

4. Searched for entries containing the closing brace `}` to locate the final fragment.

       cat server.log | grep }

5. Searched for entries containing `FLAG` to display all flag-related log messages.

       cat server.log | grep FLAG

6. Examined the output and identified the unique fragments. Some fragments appeared multiple times at different timestamps, so I treated repeated entries as duplicates.

7. Arranged the unique fragments in the correct order:

       academy{us3_
       y0urlinux_
       sk1lls_
       cedfa5fb}

8. Combined the fragments to reconstruct the complete flag.

## Commands / Tools Used

- `cat` — display the contents of a file.
- `grep` — search for lines matching a specified text pattern.
- `server.log` — the log file analyzed during the challenge.
- Linux terminal — execute commands and inspect the results.

## Key Concepts

### Log Analysis

Server logs record events and application activity. Analyzing them can help identify important information, errors, and accidentally exposed secrets.

### Pattern Matching with Grep

The `grep` command filters text by displaying lines that match a specified pattern. Searching for different parts of a flag makes it easier to locate fragments in a large log file.

### Duplicate Log Entries

The same information can appear multiple times in logs. Identifying unique fragments prevents repeated entries from being mistaken for additional parts of the flag.

### Information Disclosure

Writing sensitive information into logs can expose it to unauthorized users. Applications should avoid logging secrets and should restrict access to log files.

## Result

Successfully analyzed the server logs, identified the unique flag fragments, ignored repeated entries, and reconstructed the complete flag.

## Flag

academy{us3_y0urlinux_sk1lls_cedfa5fb}