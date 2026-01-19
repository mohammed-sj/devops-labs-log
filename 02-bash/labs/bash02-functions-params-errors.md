# *2025-10-06* **Functions — Parameters, User Input & Error Handling**

### **What I practiced**  
- Writing and calling functions
- Incorporating parameters and user inputs in functions
- Error handling
- Reading and writing files using functions
- Using and interpreting exit codes
- Verifying file authenticity through checksum

### **Cheatsheet**  
- `function_name() { commands }` | define a function
- `$#` | number of arguments passed
- `$@` | all arguments passed
- `$0` | script name
- `read var` | read user input and save it in var
- `IFS= read -r line` | safely read a line (preserve spaces, no escape handling)
- `[[ $var =~ ^[0-9]+$ ]]` | regex check if variable is numeric
- `exit 1` | exit script with non-zero (error) code
- `return <exitcode>` | set a custom exit code inside a function
- `$?` | exit status of last command (0=success, non-0=error)
- `set -e` | exit immediately if a command fails
- `set -u` | treat unset variables as an error
- `set -x` | print each command before execution (debugging)
- `set -eux` | enable all three (safe + debug mode)
- `set -o pipefail` | makes a pipeline fail if any command in it fails
- `awk '{print $2}'` | print the 2nd column from text or log
- `md5sum file` | generate MD5 checksum
- `sha256sum file` | generate SHA256 checksum
- `[[ "$a" == "$b" ]]` | compare two strings (can be used for checksum match)

---
### **Example practice**  

```bash
scholarship_eligibility(){
    echo "Enter name:"
    read -r name
    echo "Enter age:"
    read -r age

    if [ -z "$name" ]; then
        echo "Error: must enter name"
        return 1
    fi

    if [[ ! $age =~ ^[0-9]+$ ]]; then
        echo "Age must be numeric, try again"
        return 1
    elif (( age < 18 )); then
        echo "Sorry, you must be over 18 to qualify for scholarship"
        return 2
    else
        echo "Congrats $name! You are eligible for our scholarship!"
        return 0
    fi
}
scholarship_eligibility
```

```bash
file_counter(){
    local directory=$1
    local count
    count=$(ls "$directory" | wc -l)
    echo "Number of files in current directory: $count"
}

file_counter "./"
```

---

### **Key outcome**  
Learning functions felt like unlocking a new level of control. With this new tool I can:
- Structure scripts with focused functions that can be reused across tasks
- Make scripts interactive and context-aware through parameters and user input
- Identify possible failure points and use structured error handling to prevent crashes
