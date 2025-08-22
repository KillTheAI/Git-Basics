# GitHub Commands Reference

A comprehensive guide to essential Git and GitHub commands for repository management.

## Table of Contents
- [Initial Setup](#initial-setup)
- [Creating Repositories](#creating-repositories)
- [Basic Workflow](#basic-workflow)
- [Branching](#branching)
- [Remote Operations](#remote-operations)
- [Viewing History](#viewing-history)
- [Undoing Changes](#undoing-changes)
- [Stashing](#stashing)
- [Tagging](#tagging)
- [Advanced Operations](#advanced-operations)

## Initial Setup

### Configure Git (first-time setup)
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
```

### Check configuration
```bash
git config --list
git config user.name
git config user.email
```

## Creating Repositories

### Initialize a new local repository
```bash
git init
git init <directory-name>
```

### Clone an existing repository
```bash
git clone <repository-url>
git clone <repository-url> <directory-name>
git clone --branch <branch-name> <repository-url>
```

## Basic Workflow

### Check repository status
```bash
git status
git status --short  # Short format
```

### Add files to staging area
```bash
git add <file>
git add .                    # Add all files
git add *.js                 # Add all JavaScript files
git add --all                # Add all files including deleted
```

### Commit changes
```bash
git commit -m "Commit message"
git commit -am "Message"     # Add and commit tracked files
git commit --amend           # Amend last commit
```

### Push changes to remote
```bash
git push
git push origin main
git push -u origin main      # Set upstream and push
git push --force             # Force push (use with caution)
```

### Pull changes from remote
```bash
git pull
git pull origin main
git pull --rebase            # Pull with rebase instead of merge
```

## Branching

### List branches
```bash
git branch                   # List local branches
git branch -r                # List remote branches
git branch -a                # List all branches
```

### Create and switch branches
```bash
git branch <branch-name>     # Create branch
git checkout <branch-name>   # Switch to branch
git checkout -b <branch-name>  # Create and switch to branch
git switch <branch-name>     # Switch to branch (newer command)
git switch -c <branch-name>  # Create and switch to branch (newer)
```

### Delete branches
```bash
git branch -d <branch-name>  # Delete merged branch
git branch -D <branch-name>  # Force delete branch
git push origin --delete <branch-name>  # Delete remote branch
```

### Merge branches
```bash
git merge <branch-name>
git merge --no-ff <branch-name>  # No fast-forward merge
git merge --squash <branch-name> # Squash merge
```

## Remote Operations

### Manage remotes
```bash
git remote -v                # List remotes
git remote add origin <url>  # Add remote
git remote remove origin     # Remove remote
git remote rename origin upstream  # Rename remote
```

### Fetch from remote
```bash
git fetch                    # Fetch all branches
git fetch origin             # Fetch from origin
git fetch origin <branch>    # Fetch specific branch
```

## Viewing History

### View commit history
```bash
git log
git log --oneline            # Compact format
git log --graph              # Show branch graph
git log --author="Name"      # Filter by author
git log --since="2 weeks ago"  # Time-based filter
git log -n 5                 # Show last 5 commits
```

### Show differences
```bash
git diff                     # Working directory vs staging
git diff --cached            # Staging vs last commit
git diff HEAD                # Working directory vs last commit
git diff <commit1> <commit2> # Between two commits
git diff <branch1> <branch2> # Between branches
```

### Show commit details
```bash
git show <commit-hash>
git show HEAD                # Show last commit
git show --stat <commit>     # Show file statistics
```

## Undoing Changes

### Discard changes
```bash
git checkout -- <file>      # Discard working directory changes
git checkout .               # Discard all working directory changes
git restore <file>           # Restore file (newer command)
git restore .                # Restore all files
```

### Unstage files
```bash
git reset <file>             # Unstage file
git reset                    # Unstage all files
git restore --staged <file>  # Unstage file (newer command)
```

### Reset commits
```bash
git reset --soft HEAD~1      # Undo last commit, keep changes staged
git reset --mixed HEAD~1     # Undo last commit, unstage changes
git reset --hard HEAD~1      # Undo last commit, discard changes
```

### Revert commits
```bash
git revert <commit-hash>     # Create new commit that undoes changes
git revert HEAD              # Revert last commit
git revert --no-edit <commit>  # Revert without opening editor
```

## Stashing

### Stash changes
```bash
git stash                    # Stash current changes
git stash push -m "Message"  # Stash with message
git stash -u                 # Include untracked files
```

### Manage stashes
```bash
git stash list               # List all stashes
git stash show               # Show stash contents
git stash apply              # Apply last stash
git stash apply stash@{2}    # Apply specific stash
git stash pop                # Apply and remove last stash
git stash drop               # Delete last stash
git stash clear              # Delete all stashes
```

## Tagging

### Create tags
```bash
git tag <tag-name>           # Create lightweight tag
git tag -a <tag-name> -m "Message"  # Create annotated tag
git tag -a <tag-name> <commit-hash>  # Tag specific commit
```

### Manage tags
```bash
git tag                      # List tags
git tag -l "v1.*"           # List tags matching pattern
git show <tag-name>         # Show tag details
git tag -d <tag-name>       # Delete local tag
git push origin --tags      # Push all tags
git push origin <tag-name>  # Push specific tag
git push origin --delete <tag-name>  # Delete remote tag
```

## Advanced Operations

### Rebasing
```bash
git rebase main              # Rebase current branch onto main
git rebase -i HEAD~3         # Interactive rebase last 3 commits
git rebase --continue        # Continue after resolving conflicts
git rebase --abort           # Abort rebase
```

### Cherry-picking
```bash
git cherry-pick <commit-hash>  # Apply specific commit
git cherry-pick --no-commit <commit>  # Apply without committing
```

### Searching
```bash
git grep "search-term"       # Search in repository
git log --grep="pattern"     # Search commit messages
git log -S "code-string"     # Search for code changes
```

### Clean repository
```bash
git clean -n                 # Preview what will be removed
git clean -f                 # Remove untracked files
git clean -fd                # Remove untracked files and directories
git clean -fX                # Remove ignored files
```

### Aliases (shortcuts)
```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
```

## Common Workflows

### Feature branch workflow
```bash
git checkout main
git pull origin main
git checkout -b feature/new-feature
# Make changes and commits
git push -u origin feature/new-feature
# Create pull request on GitHub
# After merge:
git checkout main
git pull origin main
git branch -d feature/new-feature
```

### Hotfix workflow
```bash
git checkout main
git checkout -b hotfix/critical-fix
# Make fix and commit
git checkout main
git merge hotfix/critical-fix
git tag -a v1.0.1 -m "Hotfix version 1.0.1"
git push origin main --tags
git branch -d hotfix/critical-fix
```

## Emergency Commands

### Recover lost commits
```bash
git reflog                   # Show reference log
git checkout <commit-hash>   # Checkout lost commit
git cherry-pick <commit>     # Recover specific commit
```

### Fix detached HEAD
```bash
git checkout main            # Return to main branch
git branch temp-branch       # Create branch from current state
```

---

## Quick Reference Card

| Command | Description |
|---------|-------------|
| `git status` | Check repository status |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Commit with message |
| `git push` | Push to remote |
| `git pull` | Pull from remote |
| `git checkout -b branch` | Create and switch branch |
| `git merge branch` | Merge branch |
| `git log --oneline` | View commit history |
| `git diff` | Show changes |
| `git stash` | Temporarily save changes |

Remember to replace `<placeholders>` with actual values when using these commands!

### remove ->
