# What is Git?

Git is a **version control system** that allows you to track changes in files and projects.

Git works locally on your computer, but you can connect your local repository to services such as **GitHub, GitLab, or Gitea**. This allows you to store your repository remotely and access it from other devices.

Git also allows you to go back to previous versions of your code if you make a mistake or need to recover an earlier version.

---

# Installing and Configuring Git

Git can be downloaded from the official website:

[https://git-scm.com/](https://git-scm.com/)

Choose the appropriate version for your operating system and follow the installation instructions.

After installation, we can check the installed version with:

```bash
git --version
```

Git also needs our name and email address. This information is stored in our commits and identifies who made the changes.

We can configure them using:

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

We can check the current Git configuration with:

```bash
git config --list
```

The `--global` option means that these settings will be used for all Git repositories on our computer.

---

# Initializing a Git Repository

Before we can use Git to track a project, we need to initialize a Git repository. We do this by opening a terminal in the project's directory and running:

```bash
git init
```

This command creates a hidden `.git` directory inside the project. This directory contains all the information Git needs to track changes and manage the repository's history.

For example:

```bash
cd my-project
git init
```

After initialization, we can check the repository status with:

```bash
git status
```

The `git status` command shows which files have been modified, added, deleted, or are not yet being tracked by Git.

---

# Commits

A **commit** is a snapshot of the project at a specific point in time. It allows us to save changes to the Git history and keep track of how the project has evolved.

Before creating a commit, we first need to add the files to the **staging area**:

```bash
git add .
```

Then we create a commit with a descriptive message:

```bash
git commit -m "Add Git basics notes"
```

We can check the commit history using:

```bash
git log
```

A good commit message should briefly describe what was changed. For example:

```bash
git commit -m "Add installation instructions"
git commit -m "Fix login validation"
git commit -m "Update README"
```

Commits should be **small and focused**. Instead of making one large commit containing many unrelated changes, it is better to create separate commits for separate tasks.

---

# Staging & Committing

Git uses a **staging area** to prepare changes before they are saved in a commit. This gives us control over which changes should be included in the next commit.

First, we can check the current state of the repository:

```bash
git status
```

To add a specific file to the staging area:

```bash
git add filename.txt
```

To add all changed and new files:

```bash
git add .
```

After staging the files, we can check which files are ready to be committed:

```bash
git status
```

Finally, we create a commit:

```bash
git commit -m "Add Git notes"
```

The basic workflow looks like this:

```text
Working Directory
       ↓
   git add
       ↓
Staging Area
       ↓
  git commit
       ↓
Git Repository
```

The **working directory** contains our current files and changes. The **staging area** contains the changes we want to include in the next commit. The **repository** stores the history of our commits.

---

# File Diffs

A **diff** shows the differences between the current working version of a file and another version. It allows us to see exactly what was added, removed, or changed.

To see changes that have not been staged yet, we can use:

```bash
git diff
```

For example, if we change a line in a file, `git diff` will show the changes between the working directory and the staging area.

To see changes that are already in the staging area, we can use:

```bash
git diff --staged
```

We can also compare two commits:

```bash
git diff commit1 commit2
```

Diffs are very useful when working with Git because they allow us to **review our changes before committing them**. This helps prevent accidental changes or unwanted code from being included in a commit.

---

# Making Changes After Staging

The **staging area is not permanent**. After staging a file with `git add`, we can still modify it.

For example:

```bash
git add notes.txt
```

If we then make additional changes to `notes.txt`, Git will detect that the file is different from the staged version.

We can check the situation with:

```bash
git status
```

We may see that the file has both **staged changes** and **unstaged changes**.

To stage the latest changes again, we simply run:

```bash
git add notes.txt
```

It is important to remember that `git add` stages the current version of the file. Changes made after `git add` are not automatically included in the next commit.

---

# Commit Without Staging

Normally, we use:

```bash
git add file.txt
git commit -m "Update file"
```

However, Git also provides a shortcut for committing changes to files that are already tracked:

```bash
git commit -am "Update file"
```

The `-a` option automatically stages **modified and deleted tracked files** before creating the commit.

However, it does **not** automatically add new untracked files.

For example:

```bash
git commit -am "Update notes"
```

will not include a completely new file until we run:

```bash
git add new-file.txt
```

---

# Adding Folders

Git tracks **files**, not empty directories.

If a folder contains files, we can add the entire folder with:

```bash
git add folder/
```

For example:

```bash
git add docs/
```

This stages all files inside the `docs` directory.

We can also add multiple folders:

```bash
git add docs/ scripts/
```

If a directory is completely empty, Git will not track it. A common convention is to create a placeholder file such as:

```text
.gitkeep
```

This allows Git to track the directory because it contains a file.

`.gitkeep` has no special meaning to Git. It is simply a commonly used naming convention for placeholder files.

---

# Ignoring Files

Sometimes we don't want Git to track certain files. Examples include:

- passwords and secrets
    
- environment files
    
- log files
    
- temporary files
    
- build files
    
- dependency directories
    
- IDE configuration files
    

We can tell Git to ignore these files using a `.gitignore` file.

Example:

```text
.env
*.log
node_modules/
__pycache__/
```

We then add and commit the `.gitignore` file:

```bash
git add .gitignore
git commit -m "Add .gitignore"
```

The `.gitignore` file is especially important because it helps prevent sensitive information and unnecessary files from being added to the repository.

---

# Deleting & Restoring Files

Git can track file deletions.

We can delete a file normally:

```bash
rm notes.txt
```

Then check the repository:

```bash
git status
```

Git will show that `notes.txt` has been deleted.

We can also delete the file using Git:

```bash
git rm notes.txt
```

This removes the file from the working directory and stages the deletion at the same time.

If we want to restore a file that has been deleted but the deletion has not been staged, we can use:

```bash
git restore notes.txt
```

This restores the file to the version from the latest commit.

---

# Reverting Commits

Sometimes we make a commit that we don't want anymore. Instead of deleting the commit from history, Git allows us to create a **new commit that reverses the changes**.

This is done with:

```bash
git revert <commit>
```

For example:

```bash
git revert a1b2c3d
```

Git creates a new commit that undoes the changes introduced by the selected commit.

This is generally safer than rewriting history, especially when working with shared repositories.

---

# Git Log

The `git log` command allows us to view the history of commits in a repository.

Basic usage:

```bash
git log
```

It shows information such as:

- commit ID
    
- author
    
- date
    
- commit message
    

A more compact version is:

```bash
git log --oneline
```

Example:

```text
a1b2c3d Add Git notes
f4e5d6c Update README
789abcd Initial commit
```

The short commit ID can be used when referring to a specific commit.

We can also display a graphical history:

```bash
git log --oneline --graph --all
```

This is especially useful when working with multiple branches.

---

# Git Revert

`git revert` is used to **undo the changes introduced by an existing commit**.

For example:

```bash
git revert a1b2c3d
```

Git will create a new commit that reverses the changes from `a1b2c3d`.

The original commit remains in the history.

This is different from deleting or rewriting history. For example:

```text
A → B → C
```

After reverting commit `C`:

```text
A → B → C → C'
```

`C'` contains the changes that undo `C`.

`git revert` is useful when a commit has already been pushed to a shared remote repository because it preserves the existing history.

---

# Creating Branches

A **branch** allows us to work on a separate line of development without changing the main branch.

We can create a new branch with:

```bash
git branch feature
```

To switch to it:

```bash
git switch feature
```

We can also create and switch to a branch in one command:

```bash
git switch -c feature
```

For example:

```bash
git switch -c new-feature
```

Now we can make changes and commits without affecting the `main` branch.

We can see all branches with:

```bash
git branch
```

The current branch is marked with `*`.

Branches are commonly used for developing new features, fixing bugs, or experimenting with changes.

---

# Merging Branches

When we finish working on a branch, we can merge its changes into another branch.

First, we switch to the branch we want to merge into:

```bash
git switch main
```

Then we merge the other branch:

```bash
git merge feature
```

For example:

```text
main
  |
  A
  |
  B
   \
    C → D
       feature
```

After running:

```bash
git switch main
git merge feature
```

the changes from `feature` become part of `main`.

Sometimes Git cannot automatically combine the changes. This creates a **merge conflict**.

We then need to manually resolve the conflict, stage the resolved files, and complete the merge.

---

# Remotes

A **remote repository** is a repository stored somewhere else, usually on a remote server.

Examples include GitHub, GitLab, and Gitea.

We can see configured remotes with:

```bash
git remote -v
```

A remote is commonly called `origin`.

We can add a remote with:

```bash
git remote add origin <repository-url>
```

For example:

```bash
git remote add origin git@github.com:user/project.git
```

We can upload our local commits to the remote repository using:

```bash
git push origin main
```

To download changes from a remote repository and integrate them into the current branch:

```bash
git pull origin main
```

The basic workflow when working with a remote repository is:

```text
Working Directory
       ↓
   git add
       ↓
   git commit
       ↓
   git push
       ↓
Remote Repository
```

Git itself manages the version history, while services such as GitHub, GitLab, and Gitea provide a place to store repositories remotely and collaborate with others.