## 2025-09-29 — Bandit levels 0-15 (Linux basics to networking)

**What I practiced:**
- Securely connecting to remote servers with SSH
- Navigating directories and handling tricky filenames
- Searching for files by type, size, owner, and permissions
- Filtering and sorting text with grep, sort, uniq
- Extracting readable strings from binaries
- Decoding data (base64, ROT13, hex dumps, compressed archives)
- Using SSH keys for authentication
- Sending and receiving data over a network connection

**Why it matters:**
This set of challenges took me from the absolute basics of logging into a server, to working with search, filters, and even network communication. These levels gave me a sense of the skills that are needed for troubleshooting and automation in real systems.

**Commands *(cheatsheet)*:**
- `ssh user@host -p 2220` | connect to a remote server (using a specific port)
- `ls -la` | list all files (including hidden ones) with details
- `cat ./-filename` | read a file with a dash in its name
- `cat file\ with\ space` | read a file with a space in its name
- `find <path> -user X -group Y -size N 2>/dev/null` | search files with filter and discard errors
- `grep "string" file` | search text inside files
- `sort file` | sort text data
- `sort file | uniq -u` | show only unique lines
- `strings data.txt | grep "pattern"` | extract readable text from a binary and use it as stdn to look for pattern
- `base64 -d file` | decode base64
- `ssh -i keyfile user@host` | connect using an SSH private key
- `nc host port` | open a network connection
- `ncat --ssl localhost 30001` | open a secure network connection using SSL/TLS encryption 
- `xxd -r file` | convert hex back into binary
- `tar -xf file.tar` | extract tar archives
- `bzip2 -d file.bz2` | decompress bzip2 file (give filename .bz/.bz2 ending)
- `gzip -d file.gz` | decompress gzip file (give filename .gz ending)

**Key outcome:**  
The Linux fundamentals I practiced earlier were solidified through this set of challenges, and I also picked up new commands along the way. I became more comfortable using the man pages to explore options and apply commands more efficiently. By the end, I could handle tricky filenames, search through the filesystem, decode files, use SSH keys, and connect to network services — giving me a solid foundation that I can build on for real troubleshooting tasks in DevOps.

**Next step:**
Finish the reset of the levels (15-33)
