# *2025-11-04* — **Bash Battle Arena (Levels 1 → 10)**

### **Objective**
The Bash Battle Arena is a level based challenge designed to build Bash scripting skills through hands-on tasks. Each level focuses on a core concept from basic file management and loops to argument parsing, sorting, and monitoring. The levels gradually build up to “boss battles”, where you combine everything learned from the earlier stages into one larger script.


### **What I practiced**     
- Creating and managing files/directories
- Using variables, loops, and conditional statements
- Copying and moving files using automation instead of manual commands
- Accepting arguments from the command line and validating input
- Searching across multiple files with `grep`
- Monitoring directories in real time using `fswatch`


### **Cheatsheet**   
- `for i in {1..10}; do echo $i; done` | loop numbers 1–10  
- `if [ -f file ]; then ... fi` | check if a file exists (use `! -f` flag to check if it doesn't exist) 
- `cp Arena/*.txt Backup/` | copy all .txt files to another folder  
- `grep -l "word" *.log` | search for a word in multiple log files
- `wc -l < file.txt` | count lines in a file  
- `find dir -type f -exec ls -lh {} + | sort -k 5,5 -h` | list & sort files by size
- `fswatch -r dir` | watch a directory recursively for changes  

---

### **Boss Battle 1**   

```bash
#!/bin/bash

# The mission: 
# 1. Creates a directory names 'Battlefield'
# 2. Inside Battlefield, create files named knight.txt, sorcerer.txt, and rogue.txt.
# 3. Check if knight.txt exists; if it does, move it to a new directory called Archive.
# 4. List the contents of both Battlefield and Archive.

# The solution:

mkdir -p Battlefield
touch Battlefield/knight.txt Battlefield/sorcerer.txt Battlefield/rogue.txt

if [ -f Battlefield/knight.txt ]; then
    mkdir -p Archive
    mv Battlefield/knight.txt Archive
    echo "Knight has been moved to Archive"
else
    echo "Knight doesn't exist"
fi

echo "Listing content of Battlefield:"
ls Battlefield
echo "Listing content of Archive:"
ls Archive
```

### **Boss Battle 2**

```bash
#!/bin/bash

# The mission:
# 1. Creates a directory called Arena_Boss.
# 2. Creates 5 text files inside the directory, named file1.txt to file5.txt.
# 3. Generates a random number of lines (between 10 and 20) in each file.
# 4. Sorts these files by their size and displays the list.
# 5. Checks if any of the files contain the word 'Victory', and if found, moves the file to a directory called Victory_Archive.

# The solution:

mkdir -p Arena_Boss

for i in {1..5}; do
    FILE="Arena_Boss/file$i.txt"
    LINES=$((RANDOM % 11 + 10))
    for j in $(seq 1 $LINES); do
        echo "This is line $j" >> "$FILES"
    done
done

echo "Files sorted by size:"
find Arena_Boss -type f -exec ls -lh {} + | sort -k 5,5 -h

mkdir -p Victory_Archive
for FILE in Arena_Boss/*.txt; do
    if grep -q "Victory" "$FILE"; then
        mv "$FILE" Victory_Archive/
        echo "$FILE contains Victory and has therefore been moved to Victory_Archive"
    fi
done

```

---

### **Key outcome**
These first 10 levels helped me move from just typing single commands to actually thinking in terms of automation. I started to see how small pieces fit together into a functional, useful script. My problem-solving and understanding of how to use loops, conditionals, and file operations efficiently improved a lot through these missions, and I now feel comfortable building simple Bash workflows from scratch that handle input, sort data, and automate everyday tasks.
