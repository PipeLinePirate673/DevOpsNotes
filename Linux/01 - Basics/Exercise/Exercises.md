# Linux Basics Exercises

These exercises are based on the commands and concepts covered in `Basics`.

The goal is to practice the commands instead of only reading about them.

---

## Exercise 1 — Navigation

Start in your home directory. ✅

### Task

1. Check your current directory using `pwd`. ✅
   1. `pwd`
2. List the contents of the directory. ✅
   1. `ls`
3. Enter the `Documents` directory. ✅
   1. `cd Documents`
4. Check your current location again. ✅
   1. `pwd`
5. Go back to your home directory. ✅
   1. `cd`
6. Go to the root directory `/`. ✅
   1. `cd /`
7. Return to your home directory using `~`. ✅
   1. `cd ~`

---

## Exercise 2 — Create directories

Create the following directory structure:

```text
linux-practice/
├── files/
├── backup/
└── notes/
```

### Task

1. Create the `linux-practice` directory. ✅
   1. `mkdir linux-practice`
2. Enter it. ✅
3. Create the three directories inside it. ✅
   1. `mkdir files backup notes`
4. Use `ls -la` to check the result. ✅
   1. `ls -la`

---

## Exercise 3 — Create files

Inside the `files` directory create:

```text
file1.txt
file2.txt
file3.txt
```

### Task

1. Create all three files using one command. ✅
   1. `nano file1.txt file2.txt file3.txt`
2. Check that they exist. ✅
   1. `ls`
3. Display the detailed information about them using `ls -l`. ✅
   1. `ls -l`

---

## Exercise 4 — Copy files

Use the files from the previous exercise.

### Task

1. Copy `file1.txt` into the `backup` directory. ✅
   1. `cp file1.txt ../backups`
2. Copy `file2.txt` into the `backup` directory. ✅
   1. `cp file2.txt ../backups`
3. Check the contents of `backup`. ✅
   1. `ls backups`
4. Copy the entire `files` directory into another directory called `files-copy`. ✅
   1. `cp -r files files-copy`
   2. I need to use `-r` so it can copy directory and it content.

---

## Exercise 5 — Rename and move

### Task

1. Rename `file3.txt` to `important.txt`.  ✅
   1. `mv file3.txt important.txt`
2. Move `important.txt` into the `notes` directory. ✅
   1. `mv important.txt ../notes`
3. Check that the file is no longer inside `files`. ✅
   1. `ls`
4. Check that it exists inside `notes`. ✅
   1. `ls ../notes`

---

## Exercise 6 — Remove files

### Task

1. Create a file called `temporary.txt`. ✅
2. Check that it exists. ✅
   1. `ls`
3. Remove it using `rm`. ✅
   1. `rm remporary.txt`
4. Check that it has been removed. ✅
   1. `ls`

Then create:

```text
old-files/
├── old1.txt
├── old2.txt
└── old3.txt
```

Remove the entire `old-files` directory. ✅

`rm -r old-files`

---

## Exercise 7 — Absolute and relative paths

Assume you have this structure:

```text
linux-practice/
├── files/
│   ├── file1.txt
│   └── file2.txt
├── backup/
└── notes/
```

### Task

From different directories:

1. Navigate to `file1.txt` using a relative path. ✅
   1. `cat files/file1.txt`
2. Navigate to `notes` using a relative path. ✅
   1. `cd linux-practice/notes`
3. Navigate to `linux-practice` using an absolute path. ✅
   1. `cd Pulpit/LinuxBasicsExercises/linux-practice/`
4. Return to your home directory using `~`. ✅
   1. `cd ~`

---

## Exercise 8 — Reading files

Create a file called:

```text
notes.txt
```

Put some text inside it.

For example:

```text
Linux is an operating system kernel.
I am learning Linux for DevOps.
The terminal is one of the main tools I use.
```

### Task

1. Display the entire file using `cat`.  ✅
   1. `cat notes.txt`
2. Display the file using `less`. ✅
   1. `less notes.txt`
3. Display the first line using `head`. ✅
   1. `head -n 1 notes.txt`
4. Display the last line using `tail`. ✅
   1. `tail -n 1 notes.txt`

---

## Exercise 9 — Help

### Task

Without searching the internet:

1. Find the manual for `ls`. ✅
   1. `man ls`
   2. `ls --help`
2. Find the manual for `mkdir`. ✅
   1. `man mkdir`
   2. `mkdir --help`
3. Find the help information for `cp`. ✅
   1. `man cp`
   2. `cp --help`
4. Find the help information for `rm`. ✅
   1. `man rm`
   2. `rm --help`

Use:

```bash
man
```

and:

```bash
--help
```

---

## Exercise 10 — Package management

This exercise is for Debian/Ubuntu systems.

### Task

1. Update the package list. ✅
   1. `sudo apt update`
2. Check whether `curl` is installed. ✅
   1. `curl --version`
   2. `which curl`
3. Install `curl` if it is not installed. ✅
   1. `apt install curl`
   2. `sudo apt install curl`
4. Check the installed version. ✅
   1. `curl --version`
5. Remove `curl`. ✅
   1. `sudo apt remove curl`

Commands you may need:

```bash
apt
```

and:

```bash
curl --version
```

---

## Exercise 11 — Filesystem

Explore the basic Linux filesystem.

### Task

Check the contents of:

```text
/
```

Then find and explore:

```text
/home
/etc
/var
/tmp
/usr
/opt
/dev
/proc
```

For each directory, try to understand what kind of files or information you can find there.



1. /etc - System configuration files and scripts
2. /var - contains variable data like system logging files, files, temporary files etc.
3. /tmp - Mostly contains temporary files.
4. /usr - it contains all the user binaries, their documentation, libraries, header files, etc.
5. /opt - This directory is reserved for all the software and add-on packages
6. /dev - contains device files that represent hardware and virtual devices used by the system, such as disks, partitions, terminals, USB devices, and input devices.
7. /proc - contains virtual files that provide information about running processes and the current state of the Linux kernel and system.
8. /home - contains the personal directories and files of the system's users.


Use:

```bash
ls
```

and:

```bash
ls -la
```

---


## Exercise 12 — sudo

### Task

Try running:

```bash
apt update
```

without `sudo`.

Then try:

```bash
sudo apt update
```

### Goal

Understand why some commands require elevated privileges and why `sudo` is used. ✅

---

# Final Exercise — Linux Basics Challenge

Complete the following without looking at previous examples.

### Task

Create this structure:

```text
linux-challenge/
├── documents/
│   ├── notes.txt
│   └── todo.txt
├── backup/
└── temporary/
```

Then:

1. Navigate into `linux-challenge`. ✅

   1. `cd linux-challenge`
2. Create the required directories. ✅

   1. `mkdir documents backup temporary`
3. Create both files inside `documents`. ✅

   1. `cd documents`
   2. `nano notes.txt todo.txt`
4. Add some text to `notes.txt`.  ✅

   1. `vim notes.txt`
5. Display the contents of `notes.txt`. ✅

   1. `cat notes.txt`
6. Copy `notes.txt` into `backup`. ✅

   1. `cp notes.txt ../backup`
7. Rename `todo.txt` to `tasks.txt`. ✅

   1. `mv todo.txt tasks.txt`
8. Move `tasks.txt` into `backup`. ✅

   1. `mv tasks.txt ../backup`
9. Create a temporary file inside `temporary`. ✅

   1. `cd temporary`
   2. `nano temp.txt`
10. Remove the temporary file. ✅

    1. `rm temp.txt`
11. Display the complete directory structure using `ls -la`. ✅

    1. `ls -la`
    2. * It also depend what directory You're in. If we go back to main `linux-challenge` we can use `ls -la <dir_name>` or simply if we got `tree` installed use `tree -a`
12. Check your current location with `pwd`. ✅

    1. `pwd`
13. Go back to your home directory. ✅

    1. `cd ~`
