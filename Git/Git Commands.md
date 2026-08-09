# Git Commands

| **Command** | **What it does** | **Example** |
|---|---|---|
| `git init` | Creates a new Git repository. | `git init` |
| `git clone` | Copies an existing remote repository to your local machine, including its commit history. | `git clone <repo_url>` |
| `git status` | Shows the current state of the repository, including modified, untracked, and staged files. | `git status` |
| `git add` | Adds changes to the staging area, preparing them for the next commit. | `git add .` / `git add <file_name>` |
| `git commit` | Saves staged changes as a new commit in the local repository. | `git commit -m "Commit message"` |
| `git remote add` | Connects a local repository to a remote repository. | `git remote add origin <repo_url>` |
| `git push` | Uploads local commits to a remote repository. | `git push origin <branch_name>` |
| `git pull` | Fetches changes from a remote repository and merges them into the current branch. | `git pull` / `git pull origin <branch_name>` |
| `git fetch` | Downloads changes from a remote repository without merging them into the current branch. | `git fetch origin` |
| `git branch` | Lists, creates, or deletes branches. | `git branch` / `git branch <branch_name>` / `git branch -d <branch_name>` |
| `git checkout` | Switches branches or restores files to a previous state. | `git checkout <branch_name>` / `git checkout -b <branch_name>` |
| `git switch` | Switches between branches. It is a modern alternative to using `git checkout` for branch switching. | `git switch <branch_name>` / `git switch -c <branch_name>` |
| `git restore` | Restores files to a previous state. It is a modern alternative to using `git checkout` for restoring files. | `git restore <file_name>` / `git restore --staged <file_name>` |
| `git merge` | Combines changes from one branch into another. Git can perform a fast-forward merge or create a merge commit. | `git merge <branch_name>` |
| `git rebase` | Moves your branch on top of another branch, creating a clean, linear history without a merge commit. | `git rebase main` |
| `git log` | Displays the commit history of the current branch. | `git log` |
| `git diff` | Shows differences between different states of the repository. | `git diff` / `git diff --cached` / `git diff branch1..branch2` |
| `git reset` | Moves `HEAD` to a previous commit and can undo changes. `--soft` keeps changes staged, `--mixed` keeps them unstaged, and `--hard` removes uncommitted changes. | `git reset --soft HEAD~1` / `git reset --mixed HEAD~1` / `git reset --hard HEAD~1` |
| `git stash` | Temporarily saves uncommitted changes and returns the working directory to the last committed state. | `git stash` |
| `git stash pop` | Restores the most recently stashed changes and removes them from the stash. | `git stash pop` |
| `git clean` | Removes untracked files from the working directory. Use `-n` to preview what would be deleted. | `git clean -n` / `git clean -f` |
| `git config` | Allows you to configure Git settings at the local, global, or system level. | `git config --global user.name "Your Name"` |
| `git config --list` | Displays Git configuration settings. | `git config --list` |
| `git config --global user.name` | Sets your Git username globally. | `git config --global user.name "Your Name"` |
| `git config --global user.email` | Sets your Git email address globally. | `git config --global user.email "your@email.com"` |
