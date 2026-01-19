# *2025-10-05* **Bash - if statements & loops**

### **What I practiced**
- reading and writing scripts (if statements, for loops, while loops)
- creating arrays and accessing them
- arithmetic expansion
- setting and running script with parameters
- using control statements

###  **Cheatsheet**  
- `fruits=(apple banana orange)` | create an array
- `echo ${fruits[1]}` | access array element (index starts at 0)
- `count=42; echo $((count+1))` or `echo $((count++))` | arithmetic expansion
- `num1=5; num2=10; echo $((num1*num2))` | multiply using arithmetic expansion
- `./script.sh arg1 arg2` | run script with parameters
- `$1, $2, $@` | access first, second, or all parameters inside script
- `$(seq 1 5)` | generates range (1 to 5)
- `break` | exit the loop early
- `continue` | skip to next iteration
---

#### **If statements**  

```bash
#!/bin/bash

# basic if statement 
if [ $temp -ge 20 ]; then 
    echo "warm"
else 
    echo "cold"
fi

# if statement with multiple conditions (runs with parameters ./script.sh <grade>)
score=$1
if [ $score -ge 90 ]; then 
    echo "Excellent"; 
elif [ $score -ge 80 ]; then 
    echo "Good"; 
else
    echo "Try again" 
fi
```

---
#### **For & while loops**  

```bash
#!/bin/bash

# basic while loop (counts while condition is true)
count=1
while [ $count -le 5 ]; do 
    echo $count 
    ((count++)) 
done

# simple numeric for loop
for i in {1..5}; do 
    echo $i 
done 

# arithmetic expansion with control statement (same result as above but skips number 3)
for (( i=1; i<=5; i++ )); do
    if [ $i -eq 3 ]; then
        continue
    fi
    echo $i
done

# loop through an array
fruits=(mango kiwi apple)
for item in "${fruits[@]}";do 
    echo $item 
done
```

### **Why it matters**  
This gave me the foundation to move from running single commands to building scripts that adapt and make decisions. Knowing how variables, conditionals, and loops work lets me approach problems with automation in mind.

### **Next step**  
Finish the remainder of Bash module: 
- Functions (working with user input, parameters, and piping)
- Handling bad data and errors
