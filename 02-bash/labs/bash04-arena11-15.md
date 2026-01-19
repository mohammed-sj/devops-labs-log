# *2025-11-05* — **Bash Battle Arena (Levels 11 → 15)**

### **Objective**
These later levels of the Bash Battle Arena focus on turning small scripts into more “tool-like” utilities. The missions are about checking disk usage, parsing config files, rotating backups, and building simple menus that let the user choose what the script should do. The final boss combines several of these tasks into one menu-driven script.

---

### **What I practiced**
- Checking disk usage for a directory with `du` and thresholds  
- Reading and parsing simple `KEY=VALUE` configuration files  
- Creating compressed backups with `tar` and keeping only the most recent ones  
- Building interactive, menu-based scripts using `case` statements  
- Combining multiple utilities (disk check, uptime, backup, config parsing) into one script in Boss Battle 3  

---

### **Cheatsheet**
- `du -sm DIR` | show directory size in MB (summary)  
- `df -h` | show disk usage on each drive 
- `uptime` | show how long the system has been running  
- `tar -czf backup.tar.gz DIR` | create a compressed backup of a directory  
- `ls -t` | list files sorted by modification time (newest first)  
- `ls -t | sed -e '1,5d'` | skip the 5 newest files (used to delete older backups)  
- `while IFS= read -r file; do ...; done` | loop safely over lines from stdin  
- `while IFS='=' read -r key value; do ...; done < settings.conf` | read settings line by line and split each at '='
- `cut -d: -f1 /etc/passwd` | list usernames on the system (uses ":" as field seperator and keeps the first column)
- `case $choice in ... esac` | menu-style branching based on user input  

---

### **Boss Battle 3**

```bash
#!/bin/bash

# The mission:
# 1. Present a menu to the user with options:
#    - Check disk space
#    - Show system uptime
#    - Backup the Arena directory and keep the last 3 backups
#    - Parse a configuration file settings.conf and display the values
# 2. Execute the chosen task.

echo "Choose an option:"
echo "1. Check disk space"
echo "2. Show system uptime"
echo "3. Backup Arena directory (keep last 3 backups)"
echo "4. Parse configuration file (settings.conf)"

read -rp "Enter your choice [1-4]: " choice

case "$choice" in
    1)
        echo "Disk space:"
        df -h
        ;;
    2)
        echo "System uptime:"
        uptime
        ;;
    3)
        SOURCE_DIR="Arena"
        BACKUP_DIR="Backups"

        mkdir -p "$BACKUP_DIR"

        TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")
        BACKUP_NAME="backup_$TIMESTAMP.tar.gz"

        tar -czf "$BACKUP_DIR/$BACKUP_NAME" "$SOURCE_DIR"
        echo "Created backup: $BACKUP_NAME"

        ls -t "$BACKUP_DIR" | sed -e '1,3d' | while IFS= read -r file; do
            rm -f "$file"
            echo "Deleted old backup: $file"
        done
        ;;
    4)
        CONFIG_FILE="settings.conf"

        if [ ! -f "$CONFIG_FILE" ]; then
            echo "Configuration file '$CONFIG_FILE' does not exist."
            exit 1
        fi

        while IFS='=' read -r key value; do
            echo "Key: $key, Value: $value"
        done < "$CONFIG_FILE"
        ;;
    *)
        echo "Invalid option"
        ;;
esac
```

---

### **Key outcome**   
I learned how to check disk usage, manage backups safely, and make my scripts more flexible rather than hardcoded. Building a menu-driven “mini tool” in Boss Battle 3 helped me see how several simple scripts can be combined into one practical, reusable Bash script.
