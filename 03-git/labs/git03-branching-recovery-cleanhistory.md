# 2025-11-17 — Branching, Recovery & Clean History

## What I Practiced
- Creating and merging branches, resolving merge conflicts manually.
- Using Git workflows (feature branches, pull requests, approvals).
- Undoing changes safely with `restore`, `reset`, and `revert`.
- Temporarily saving work with git stash.
- Cleaning commit history using rebase and squash.
- Applying commits across branches with cherry-pick.
- Protecting secrets and large files using .gitignore.
- Fixing or extending the last commit with git commit --amend.
- Automating code checks with pre-commit hooks.

## Cheatsheet
- `git checkout -b <branch>` | create and switch to a new branch
- `git restore <file>` | undo unstaged file changes
- `git revert HEAD` | safely undo most recently pushed commit
- `git stash push -m "<msg>"` | temporarily store uncommitted changes
- `git stash apply / pop` | restore or restore+remove stashed changes
- `git rebase -i HEAD~3` | squash or reorder commits (latest 3)
- `git cherry-pick <commit_id>` | apply a commit from another branch
- `echo ".env" >> .gitignore` | exclude sensitive files
- `git commit --amend` | modify the previous commit message or content
- `pre-commit install` | enable hooks in current repo

## Key Outcome
I learned to manage Git history in a more intentional way using branching, undoing, rebasing, and automating code quality checks. Commands that used to feel like “rescue tools” now feel like part of a clean, collaborative workflow. 
