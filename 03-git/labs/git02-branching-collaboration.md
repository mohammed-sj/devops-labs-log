# *2025-11-10* **Branching, Collaboration & Advanced Git Tools**

### What I practiced   
- Understanding the difference between Git (tool) and GitHub (platform).
- Understanding how merge types (fast-forward vs recursive) work and how conflicts are resolved.
- Visualizing branches and commits 
- Explored how rebase, stash, and cherry-pick are used to keep history clean and flexible
- Comparing reset vs revert and knowing when each is safe to use.
- Understanding collaborative workflows: forks, pull requests, and code reviews.
- Theory behind good branching practices and exploring trunk-based development.

### Cheatsheet   

* `git branch` | List or create branches
* `git switch -c <BRANCH>` | Create and switch to a new branch
* `git merge <BRANCH>` | Merge a branch into the current one
* `git rebase <BRANCH>` | Reapply commits on top of another branch
* `git stash` | Temporarily store uncommitted work
* `git stash pop` | Reapply and remove the most recent stash
* `git reset --soft|mixed|hard` | Move HEAD and optionally unstage or delete changes
* `git revert <COMMIT>` | Safely undo a commit by creating a new one
* `git cherry-pick <COMMIT>` | Apply a single commit from another branch
* `git pull` | Fetch and merge changes from remote
* `git push origin <BRANCH>` | Push local branch to GitHub
* `git log --graph --oneline --all` | Visualize full branch and merge history

### Key outcome   
Built a solid understanding of how branching, merging, and pull requests fit into real collaboration.
Learned how rebase, stash, and cherry-pick help keep history organized and workflows clean when managing multiple branches.
