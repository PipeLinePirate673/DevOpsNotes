# Chapter 2 --- Files and Directories

The goal of this chapter is to understand how Linux handles files and
directories, and how to create, copy, move, rename, delete, search, and
inspect them.

---

## 1. Files vs Directories

In Linux, almost everything is treated as a **file**.

Examples:

```text
file.txt
script.sh
image.jpg
directory/
```

A directory is a place where other files and directories are stored.

Example:

```text
home/
└── dominik/
    ├── Documents/
    │   ├── notes.txt
    │   └── todo.txt
    ├── Downloads/
    └── Pictures/
```

---

## 2. `ls` --- List Files and Directories

Basic:

```bash
ls
```

Detailed information:

```bash
ls -l
```

Show hidden files:

```bash
ls -a
```

Combine options:

```bash
ls -la
```

Human-readable file sizes:

```bash
ls -lh
```

You can also specify a directory:

```bash
ls -la Documents
```

---

## 3. `mkdir` --- Create Directories

Create one directory:

```bash
mkdir projects
```

Create multiple directories:

```bash
mkdir projects backups scripts
```

Create an entire directory structure:

```bash
mkdir -p projects/linux/scripts
```

The `-p` option creates the parent directories if they do not already
exist.

---

## 4. `touch` --- Create Files

Create an empty file:

```bash
touch notes.txt
```

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

`touch` can also update the timestamp of an existing file.

Important:

```bash
touch notes.txt
```

does **not** delete the existing contents of `notes.txt`.

---

## 5. `cp` --- Copy Files and Directories

Copy a file:

```bash
cp notes.txt backup/
```

Copy and rename at the same time:

```bash
cp notes.txt backup.txt
```

Copy multiple files:

```bash
cp file1.txt file2.txt backup/
```

Copy a directory:

```bash
cp -r files/ backup/
```

### Important

`-r` means **recursive**.

It tells Linux to copy the directory and everything inside it.

---

## 6. `mv` --- Move and Rename

Move a file:

```bash
mv notes.txt Documents/
```

Rename a file:

```bash
mv old.txt new.txt
```

Move and rename at the same time:

```bash
mv old.txt Documents/new.txt
```

Remember:

> `mv` is used for both **moving** and **renaming**.

---

## 7. `rm` --- Remove Files

Remove a file:

```bash
rm notes.txt
```

Remove multiple files:

```bash
rm file1.txt file2.txt
```

Remove a directory and its contents:

```bash
rm -r old-files/
```

### Be careful with:

```bash
rm -rf
```

`-r` = recursive
`-f` = force

This can remove a large amount of data very quickly without asking for
confirmation.

---

## 8. `rmdir` --- Remove Empty Directories

```bash
rmdir empty-directory
```

`rmdir` only works when the directory is empty.

For example:

```text
empty/
```

can be removed with:

```bash
rmdir empty
```

But:

```text
files/
├── file1.txt
└── file2.txt
```

cannot be removed using `rmdir`.

---

## 9. Paths

Understanding paths is one of the most important Linux concepts.

### Absolute path

An absolute path starts with `/`.

Example:

```text
/home/dominik/Documents/notes.txt
```

It describes the complete path starting from the root directory.

### Relative path

A relative path depends on your current directory.

If you are in:

```text
/home/dominik/
```

then:

```text
Documents/notes.txt
```

points to:

```text
/home/dominik/Documents/notes.txt
```

---

## 10. `pwd` --- Print Working Directory

The `pwd` command shows your current working directory.

```bash
pwd
```

Example:

```text
/home/dominik/Documents
```

This is especially useful when working with relative paths because it
shows exactly where you currently are.

---

## 11. `cd` --- Change Directory

The `cd` command is used to move between directories.

Enter a directory:

```bash
cd Documents
```

Use an absolute path:

```bash
cd /var/log
```

Go to the parent directory:

```bash
cd ..
```

Go to your home directory:

```bash
cd ~
```

Return to the previous directory:

```bash
cd -
```

For example:

```bash
cd /var/log
cd /tmp
cd -
```

The last command returns you to:

```text
/var/log
```

---

## 12. `.` --- Current Directory

The dot:

```text
.
```

means **current directory**.

Example:

```bash
cp notes.txt ./backup/
```

This means:

> Copy `notes.txt` into the `backup` directory inside the current
> directory.

---

## 13. `..` --- Parent Directory

The double dot:

```text
..
```

means **parent directory**.

If you are in:

```text
/home/dominik/Documents/
```

then:

```bash
cd ..
```

takes you to:

```text
/home/dominik/
```

You can also use it with other commands:

```bash
cp notes.txt ../backup/
```

This means:

> Copy `notes.txt` into the `backup` directory one level above the
> current directory.

---

## 14. `~` --- Home Directory

```bash
cd ~
```

takes you to your home directory.

You can also use `~` in paths:

```bash
~/Documents
```

For example:

```text
/home/dominik/Documents
```

---

## 15. `file` --- Check File Type

You can use `file` to find out what type of file something actually is.

```bash
file notes.txt
```

For example:

```text
ASCII text
```

Another example:

```bash
file image.jpg
```

might return something like:

```text
JPEG image data
```

Linux does not rely only on file extensions to determine what a file is.

---

## 16. `stat` --- Detailed File Information

```bash
stat notes.txt
```

This provides information such as:

* file size
* permissions
* owner
* timestamps
* inode
* access information

You will use some of this information later when learning **file
permissions**.

---

## 17. Hidden Files

In Linux, files beginning with `.` are hidden.

Examples:

```text
.bashrc
.gitconfig
.profile
```

Running:

```bash
ls
```

may not show them.

To show hidden files:

```bash
ls -a
```

---

## 18. `tree` --- Display Directory Structure

If `tree` is installed:

```bash
tree
```

Example:

```text
linux-practice
├── backup
│   ├── file1.txt
│   └── file2.txt
├── files
│   ├── file1.txt
│   └── file2.txt
└── notes
    └── important.txt
```

Show hidden files as well:

```bash
tree -a
```

---

## 19. `find` --- Search for Files

Search for `notes.txt` starting from the current directory:

```bash
find . -name "notes.txt"
```

Find all `.txt` files:

```bash
find . -name "*.txt"
```

Find directories:

```bash
find . -type d -name "backup"
```

Find files:

```bash
find . -type f
```

`find` is an important tool to learn, especially for DevOps and system
administration.

---

## 20. `du` --- Directory and File Sizes

Check directory sizes:

```bash
du -h
```

Check the total size of a specific directory:

```bash
du -sh Documents
```

`-s` = summary
`-h` = human-readable

Example:

```text
2.4G    Documents
```

---

## 21. `df` --- Disk Space

Check filesystem disk usage:

```bash
df -h
```

Example:

```text
Filesystem      Size  Used Avail Use%
/dev/sda2       100G   65G   30G  69%
```

The difference between `du` and `df` is important:

```text
du → how much space files/directories use

df → how much space is available on a filesystem
```

---

## 22. `ln` --- Create Links

Linux allows you to create links to files.

There are two main types:

* **hard links**
* **symbolic links (symlinks)**

### Hard link

```bash
ln file.txt hardlink.txt
```

A hard link points to the same underlying file data.

### Symbolic link

```bash
ln -s file.txt symlink.txt
```

A symbolic link works like a reference or shortcut to another file or
directory.

For example:

```text
file.txt
symlink.txt -> file.txt
```

You will learn more about links and inodes later when working with
filesystems and permissions.

---

# Four Path Symbols to Remember

```text
/       → root directory
~       → home directory
.       → current directory
..      → parent directory
```


```
