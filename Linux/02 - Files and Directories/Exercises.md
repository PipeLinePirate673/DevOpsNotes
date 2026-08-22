# Linux Practice — Files and Directories

# Linux Practice — Files and Directories

## Exercise 1 — Project Structure ✅

Create a directory named `linux-practice`.

Inside it, create the following structure:

```text
linux-practice/
├── projects/
├── backups/
├── notes/
└── scripts/
```

### PLACE FOR YOUR NOTES/COMMAND LIST

```bash
mkdir -p linux-practice/projects linux-practice/backups linux-practice/notes linux-practice/scripts
```

---

## Exercise 2 — Organize Files ✅

Inside `linux-practice`, create these files:

```text
notes.txt
commands.txt
todo.txt
```

Then organize them so that:

```text
linux-practice/
├── notes/
│   └── notes.txt
├── scripts/
│   └── commands.txt
└── todo.txt
```

### PLACE FOR YOUR NOTES/COMMAND LIST

```bash
touch notes/notes.txt scripts/commands.txt todo.txt
```

---

## Exercise 3 — Nested Project ✅

Inside `projects`, create:

```text
projects/
└── linux/
    ├── files/
    ├── directories/
    └── scripts/
```

### PLACE FOR YOUR NOTES/COMMAND LIST

```bash
mkdir -p projects/linux/files projects/linux/directories projects/linux/scripts
```

---

## Exercise 4 — Backup ✅

Create a backup of the entire `projects` directory.

The backup should be located inside:

```text
backups/
```

The original `projects` directory must remain unchanged.

### PLACE FOR YOUR NOTES/COMMAND LIST

```bash
cp -r projects/ backups/
```

---

## Exercise 5 — Rename ✅

Rename:

```text
todo.txt
```

to:

```text
tasks.txt
```

Then rename the `scripts` directory to:

```text
bash
```

### PLACE FOR YOUR NOTES/COMMAND LIST

```bash
mv todo.txt tasks.txt
mv scripts/ bash/
```

---

## Exercise 6 — Hidden File ✅

Create a hidden file named:

```text
.config
```

inside `linux-practice`.

Make sure it is not visible with a normal directory listing but can still be found when hidden files are displayed.

### PLACE FOR YOUR NOTES/COMMAND LIST

```bash
touch .config
```

---

## Exercise 7 — File Search ✅

Create the following files inside `linux-practice`:

```text
README.txt
backup.txt
```

Then search the entire `linux-practice` directory for files ending in `.txt`.

### PLACE FOR YOUR NOTES/COMMAND LIST

```bash
find . -name "*.txt"
```

---

## Exercise 8 — File Information ✅

Choose one of the files you created.

Find out:

* its file type
* its size
* its owner
* its permissions
* its modification time

### PLACE FOR YOUR NOTES/COMMAND LIST

```bash
stat notes/notes.txt
```

---

## Exercise 9 — Directory Size ✅

Check how much disk space is being used by:

```text
projects/
backups/
linux-practice/
```

Identify which directory uses the most space.

### PLACE FOR YOUR NOTES/COMMAND LIST

```bash
du -sh projects/
du -sh backups/
du -sh .
```

---

## Exercise 10 — Filesystem Usage ✅

Check the current filesystem usage.

Identify:

* total disk space
* used space
* available space
* filesystem containing your current directory

### PLACE FOR YOUR NOTES/COMMAND LIST

```bash
df -h
```

---

## Exercise 11 — Cleanup

Remove the following:

```text
backup.txt
projects/linux/files/
```

The rest of the project must remain untouched.

### PLACE FOR YOUR NOTES/COMMAND LIST

```text

```

---

## Exercise 12 — Empty Directory

Create a directory named:

```text
temporary
```

Make sure it remains empty.

Remove it afterwards using `rmdir`.

### PLACE FOR YOUR NOTES/COMMAND LIST

```text

```

---

## Exercise 13 — Backup Update

The original `projects` directory has now been modified.

Create a new backup of the current `projects` directory inside:

```text
backups/
```

Replace the old backup with the new one.

The final backup should reflect the current contents of `projects`.

### PLACE FOR YOUR NOTES/COMMAND LIST

```text

```

---

## Exercise 14 — Final Verification

Verify the final structure of `linux-practice`.

Your final structure should look like:

```text
linux-practice/
├── .config
├── README.txt
├── backups/
│   └── projects/
│       └── linux/
│           ├── directories/
│           └── scripts/
├── bash/
│   └── commands.txt
├── notes/
│   └── notes.txt
├── projects/
│   └── linux/
│       ├── directories/
│       └── scripts/
└── tasks.txt
```

Verify that:

* all required directories exist
* all required files exist
* `.config` exists
* `README.txt` exists
* `tasks.txt` exists
* `bash/commands.txt` exists
* the backup contains the current `projects` structure
* `projects/linux/files/` no longer exists
* `temporary/` does not exist
* no unwanted files remain
* the directory structure matches the expected result

Useful commands:

```bash
ls -la
tree -a
find . -type f
find . -type d
```

### PLACE FOR YOUR NOTES/COMMAND LIST

```text

```

## Exercise 1 — Project Structure ✅

Create a directory named `linux-practice`.

Inside it, create the following structure:

```text
linux-practice/
├── projects/
├── backups/
├── notes/
└── scripts/
```

### PLACE FOR YOUR NOTES/COMMAND LIST

`mkdir -p linux-practice/projects linux-practice/backups linux-practice/notes linux-practice/scripts`

---

## Exercise 2 — Organize Files ✅

Inside `linux-practice`, create these files:

```text
notes.txt
commands.txt
todo.txt
```

Then organize them so that:

```text
linux-practice/
├── notes/
│   └── notes.txt
├── scripts/
│   └── commands.txt
└── todo.txt
```

### PLACE FOR YOUR NOTES/COMMAND LIST

`touch notes/notes.txt scripts/commands.txt todo.txt`

## Exercise 3 — Nested Project ✅

Inside `projects`, create:

```text
projects/
└── linux/
    ├── files/
    ├── directories/
    └── scripts/
```

### PLACE FOR YOUR NOTES/COMMAND LIST

`mkdir -p projects/linux/files projects/linux/directories projects/linux/scripts`

---

## Exercise 4 — Backup ✅

Create a backup of the entire `projects` directory.

The backup should be located inside:

```text
backups/
```

The original `projects` directory must remain unchanged.

### PLACE FOR YOUR NOTES/COMMAND LIST

`cp -r projects/ backups/`

---

## Exercise 5 — Rename ✅

Rename:

```text
todo.txt
```

to:

```text
tasks.txt
```

Then rename the `scripts` directory to:

```text
bash
```

### PLACE FOR YOUR NOTES/COMMAND LIST

`mv todo.txt tasks.txt`

`mv scripts/ bash/`

---

## Exercise 6 — Hidden File ✅

Create a hidden file named:

```text
.config
```

inside `linux-practice`.

Make sure it is not visible with a normal directory listing but can still be found when hidden files are displayed.

### PLACE FOR YOUR NOTES/COMMAND LIST

`mkdir .config`

---

## Exercise 7 — File Search ✅

Create the following files in different directories:

```text
README.txt
notes.txt
commands.txt
backup.txt
```

Search the entire `linux-practice` directory for files ending in `.txt`.

### PLACE FOR YOUR NOTES/COMMAND LIST

`find -name "*.txt"`

---

## Exercise 8 — File Information ✅

Choose one of the files you created.

Find out:

- its file type
- its size
- its owner
- its permissions
- its modification time

### PLACE FOR YOUR NOTES/COMMAND LIST

`stat notes.txt`

---

## Exercise 9 — Directory Size ✅

Check how much disk space is being used by:

```text
projects/
backups/
linux-practice/
```

Identify which directory uses the most space.

### PLACE FOR YOUR NOTES/COMMAND LIST

`du -sh projects`

`du -sh backups/`

`du -sh ..`

---

## Exercise 10 — Filesystem Usage ✅

Check the current filesystem usage.

Identify:

- total disk space
- used space
- available space
- filesystem containing your current directory

### PLACE FOR YOUR NOTES/COMMAND LIST

`df -h`

---

## Exercise 11 — Cleanup ✅

Remove the following files and directories:

```text
commands.txt
projects/linux/files/
```

The rest of the project must remain untouched.

### PLACE FOR YOUR NOTES/COMMAND LIST

`rm bash/commands.txt`

`rmdir projects/linux/files`

---

## Exercise 12 — Empty Directory ✅

Create a directory named:

```text
temporary
```

Make sure it remains empty.

Remove it afterwards.

### PLACE FOR YOUR NOTES/COMMAND LIST

`mkdir temporary`

`rmdir temporary`

---

## Exercise 13 — Directory Structure ✅

Create the following final structure:

```text
linux-practice/
├── .config
├── backups/
│   └── projects/
│       └── linux/
│           ├── directories/
│           └── scripts/
├── notes/
│   └── notes.txt
├── projects/
│   └── linux/
│       ├── directories/
│       └── scripts/
├── scripts/
│   └── bash/
└── tasks.txt
```

Do not recreate the directory from scratch.

Build this structure using the files and directories you already created during the previous exercises.

### PLACE FOR YOUR NOTES/COMMAND LIST

`dominik@Zenbook:~/Pulpit/LinuxBasicsExercises/linux-practice$ tree -a . ├── backups │   └── projects │       └── linux │           ├── directories │           └── scripts ├── .config ├── notes │   └── notes.txt ├── projects │   └── linux │       ├── directories │       └── scripts ├── scripts │   └── bash └── tasks.txt`

---

## Exercise 14 — Final Verification ✅

Verify the final structure of `linux-practice`.

Check that:

- all required directories exist
- all required files exist
- `.config` exists
- the backup contains the required project files
- no unwanted files remain
- the directory structure matches the expected result

### PLACE FOR YOUR NOTES/COMMAND LIST

`This Exercise is a little bit messy and not good made. I have to rewrite it in near feature.`
