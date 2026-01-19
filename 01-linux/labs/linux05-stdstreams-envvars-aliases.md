## 2025-09-28 — Standard streams, environment variables & aliases

**What I practiced:**  
- How Linux handles input and output through the three standard streams: stdin, stdout, and stderr
- Redirecting output and errors into files
- Setting and viewing environment variables
- Making simple shortcuts for commands (aliases)
 
**Why it matters:**  
These concepts are essential in controlling how the shell behaves:
- By understanding streams I can control where data goes, which is crucial for scripting and logging 
- Environment variables shape how the system works
- Aliases save time by cutting down on repetitive typing   
These skills form a foundation that is needed for scripting, automating tasks, and customizing the Linux environment.

**Commands (*cheatsheet*):**  
- `./script.sh < file.txt` | use a file as input
- `ls nonexistent 2> error.txt` | redirect errors to a file
- `ls dir nonexistent &> all.txt` | redirect both output and errors
- `ls nonexistent 2> /dev/null` | discard errors completely
- `printenv` / `env` | list environment variables
- `echo $HOME` | show the value of a variable
- `export VAR="value"` | set an environment variable for this session (add to .zshrc to make permanent)
- `source ~/.zshrc` | reload settings
- `alias` | list aliases
- `alias ll='ls -lah'` | shortcut for detailed directory listing

**Key outcome:**  
I understand how Linux handles input, output, and errors, and how to control them.
I can view and set environment variables, make them permanent, and create useful shortcuts with aliases.
The terminal now feels more customizable and easier to work with.
  
**Next step:**  
Start working through OverTheWire Bandit wargames (lvl 1-15) and apply what I've practiced so far in the Linux fundamentals module


