# Linux Basics

This is my starting point for learning Linux.

Here I keep the basic things I need to understand before moving to more advanced topics.

---

## What is Linux?

Linux is an operating system kernel. Different Linux distributions use the Linux kernel together with other software to create a complete operating system.

Examples of Linux distributions:

* Ubuntu
* Debian
* Fedora
* Arch Linux
* Linux Mint
* Alpine Linux

For my learning I mainly use Linux for practicing DevOps, servers, containers and automation.

---

## Terminal

The terminal is one of the main ways to interact with Linux.

Instead of clicking through graphical interfaces, I can use commands to control the system.

For example:

```bash
pwd
```

shows where I currently am.

```bash
ls
```

shows what is inside the current directory.

```bash
cd Documents
```

moves me into the `Documents` directory.

---

## Shell

The shell is the program that interprets the commands I type in the terminal.

One of the most common shells on Linux is **Bash**.

Example:

```bash
echo "Hello Linux"
```

Bash takes the command and executes it.

> Bash will be covered separately in my `Bash` section.

---

# Navigation

Understanding how to move around the filesystem is one of the first things I need to learn.

## `pwd`

`pwd` means **Print Working Directory**.

It shows my current location.

```bash
pwd
```

Example:

```text
/home/dominik
```

---

## `ls`

`ls` lists files and directories.

```bash
ls
```

Useful options:

```bash
ls -l
```

Shows more information about files.

```bash
ls -a
```

Shows hidden files.

```bash
ls -la
```

Shows hidden files together with detailed information.

---

## `cd`

`cd` means **Change Directory**.

It is used to move between directories.

```bash
cd Documents
```

Go into `Documents`.

```bash
cd ..
```

Go one directory up.

```bash
cd ~
```

Go to my home directory.

```bash
cd /
```

Go to the root directory.

---

# Paths

Linux uses paths to describe the location of files and directories.

### Absolute path

An absolute path starts from `/`.

Example:

```text
/home/dominik/Documents/file.txt
```

It describes the complete location of the file.

### Relative path

A relative path starts from my current location.

Example:

```text
Documents/file.txt
```

The meaning depends on where I currently am.

---

## Important path symbols


| Symbol | Meaning           |
| ------ | ----------------- |
| `/`    | Root directory    |
| `~`    | Home directory    |
| `.`    | Current directory |
| `..`   | Parent directory  |

Examples:

```bash
cd ..
```

Move one level up.

```bash
cd ./Documents
```

Go to `Documents` from the current directory.

```bash
cd ~/Documents
```

Go to `Documents` inside my home directory.

---

# Creating directories

## `mkdir`

`mkdir` means **Make Directory**.

```bash
mkdir test
```

Creates a directory called `test`.

I can also create multiple directories:

```bash
mkdir one two three
```

Create nested directories:

```bash
mkdir -p projects/linux/basics
```

The `-p` option creates the missing parent directories as well.

---

# Creating files

## `touch`

`touch` can be used to create an empty file.

```bash
touch file.txt
```

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

---

# Copying files

## `cp`

`cp` means **copy**.

```bash
cp file.txt backup.txt
```

This creates a copy of `file.txt` called `backup.txt`.

Copy a file to another directory:

```bash
cp file.txt Documents/
```

Copy a directory:

```bash
cp -r folder1 folder2
```

The `-r` option means recursive and is needed when copying directories.

---

# Moving and renaming

## `mv`

`mv` is used to move or rename files and directories.

Rename a file:

```bash
mv old.txt new.txt
```

Move a file:

```bash
mv file.txt Documents/
```

Move and rename at the same time:

```bash
mv file.txt Documents/new-name.txt
```

---

# Removing files

## `rm`

`rm` removes files.

```bash
rm file.txt
```

Remove a directory and its contents:

```bash
rm -r folder
```

### Be careful

Linux normally does not move files deleted with `rm` to a recycle bin.

This command can permanently remove data.

I should always check what I am deleting before using:

```bash
rm
```

or especially:

```bash
rm -rf
```

---

# Reading files

## `cat`

`cat` displays the contents of a file.

```bash
cat file.txt
```

---

## `less`

`less` allows me to read larger files page by page.

```bash
less file.txt
```

I can move through the file and exit with:

```text
q
```

---

## `head`

Shows the beginning of a file.

```bash
head file.txt
```

Show the first 20 lines:

```bash
head -n 20 file.txt
```

---

## `tail`

Shows the end of a file.

```bash
tail file.txt
```

Show the last 20 lines:

```bash
tail -n 20 file.txt
```

---

# Finding help

Linux provides several ways to find information.

## `man`

`man` shows the manual for a command.

```bash
man ls
```

For example:

```bash
man mkdir
```

I can read what the command does and see its available options.

Press:

```text
q
```

to exit.

---

## `--help`

Many commands also provide a shorter help message.

```bash
ls --help
```

or:

```bash
mkdir --help
```

This is often faster than opening the full manual.

---

# sudo

`sudo` allows me to execute a command with elevated privileges.

For example:

```bash
sudo apt update
```

Some operations require administrator privileges.

I should not use `sudo` automatically for every command.

---

# Package management

Package management depends on the Linux distribution.

On Debian and Ubuntu systems I can use `apt`.

Update the package list:

```bash
sudo apt update
```

Upgrade installed packages:

```bash
sudo apt upgrade
```

Install a package:

```bash
sudo apt install nginx
```

Remove a package:

```bash
sudo apt remove nginx
```

---

# Basic Linux filesystem

Linux has a standard filesystem structure.

Some important directories:


| Directory | What I find there                                  |
| --------- | -------------------------------------------------- |
| `/`       | Root of the filesystem                             |
| `/home`   | Users' home directories                            |
| `/root`   | Home directory of the root user                    |
| `/etc`    | System configuration files                         |
| `/var`    | Variable data such as logs                         |
| `/tmp`    | Temporary files                                    |
| `/usr`    | User programs and system resources                 |
| `/bin`    | Essential commands                                 |
| `/dev`    | Device files                                       |
| `/proc`   | Information about running processes and the kernel |
| `/opt`    | Optional/additional software                       |



---

# What I learned

After this section I should be comfortable with:

* using the terminal
* understanding the difference between Linux and the shell
* navigating the filesystem
* understanding absolute and relative paths
* creating files and directories
* copying files
* moving and renaming files
* deleting files
* reading files
* finding command documentation
* understanding basic `sudo` usage
* installing packages with `apt`
* recognizing the most important Linux directories
