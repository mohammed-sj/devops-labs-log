## 2025-10-02 — Bandit levels 16-33 (privilege, scripts & git)

**What I practiced:**  
- Executing commands remotely over ssh
- Assigning variables to strings and to command output
- Changing permissions on files and directories
- Reading and writing a simple script
- Brute forcing with a for loop script
- Using interactive programs (like more and vim) to escape a restricted shell and spawn a normal bash shell
- Basic git commands

**Why it matters:**  
Working through these levels meant combining several smaller Linux and Git skills into practical problem-solving. I had to automate repetitive tasks with scripts, adjust permissions to access files, and dig through repository history for hidden information. Practicing these kinds of situations step by step gave me more confidence using the shell for real work.

**Commands (*cheatsheet*):**  
- `diff passwords.old passwords.new` | compare two files line by line  
- `./<suid> <command> <argument>` | run a program with file owner’s privileges 
- `nc -l <port>` | start a TCP listener on a port  
- `var=$(command)` | assign the output of `command` to the shell variable `var`  
- `chmod +rwx <file/directory>` | add read, write and execute permissions to a file or directory  
- `chmod 421 <file/directory>` | set permissions: owner=read (4), group=write (2), others=execute (1)
- `:set shell=/bin/bash` | set default shell as /bin/bash in vim 
- `:shell` | spawn user's default shell 
- `git clone <repo>` | clone a Git repository
- `git log` | view commit history
- `git show <commit or tag>` | show contents of a specific commit or tag
- `git branch -a` | list all local and remote branches
- `git checkout` | switch to existing local branch
- `git tag` | list tags in repo
- `git add -f <file>` | add files (even if its ignored)
- `git commit -m <message>` | record changes to repo & add message
- `git push` | push commit to remote repo 

**For loop script used:**  
```bash
#!/bin/bash

for i in {0000..9999}
do
        echo gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i >> brute.txt
done

cat brute.txt | nc localhost 30002
```
**Key outcome:**  
I was able to escape a restricted shell into a normal bash environment, which opened up access to the full system. I also wrote a simple loop to brute-force a 4-digit service password and confirmed it worked by getting the expected response. On the Git side, I used git log and git show to inspect old commits and tags until I found the information needed. Altogether, these steps gave me a clearer sense of how to mix scripting, permissions, and version control when solving problems.
 
**Next step:**  
Begin mini-project
