## *2025-09-26* — Vim navigation & text editing

**What I practiced:**
- Switching between different modes
- Navigating text more efficiently
- Copying, pasting, and deleting more efficiently
- Saving and quitting

**Why it matters:**   
Becoming proficient in VIM enhances productivity by making navigation and text editing a smoother process. It’s also essential for working with configuration files, logs, and scripts directly on servers where no GUI is available.

**Shortcuts inside Vim:**
- `i` | enter insert mode
- `v` | enter visual mode
- `Esc` | go back to command mode
- `:w` | save
- `:wq!` | save + quit
- `:q!` | quit without saving
- `dd` | delete line
- `D` | delete from cursor to end of line
- `yy` | copy (yank) line
- `p` | paste
- `u` | undo
- `Ctrl+r` | redo
- `0` | jump to start of line
- `$` | jump to end of line
- `w` | jump forward by a word
- `b` | jump back by a word 
- `/word` | search for word
- `n` | next match
- `N` | previous match
- `:set number` | show line numbers (nonumber to hide)
- `:syntax on` | enable syntax highlighting


**Key outcome:**  
Before: I had to rely on arrow keys to navigate text.  
After: Editing and navigation are much smoother and less time-consuming. I can see how this helps the flow of work, since I don’t get stuck just moving around a file.  

**Reflection (next step):**  
I'll practice until the commands become muscle memory, and add a cheatsheet file I can open inside Vim with `:e ~/vim-cheatsheet.txt` for quick reference.
