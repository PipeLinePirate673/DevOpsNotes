# Linux Basics Exercises

These exercises are based on the commands and concepts covered in
`Basics`.

The goal is to practice the commands instead of only reading about them.

------------------------------------------------------------------------

## Exercise 1 --- Navigation

Start in your home directory.

### Task

1.  Check your current directory using `pwd`.
2.  List the contents of the directory.
3.  Enter the `Documents` directory.
4.  Check your current location again.
5.  Go back to your home directory.
6.  Go to the root directory `/`.
7.  Return to your home directory using `~`.

------------------------------------------------------------------------

## Exercise 2 --- Create directories

Create the following directory structure:

``` text
linux-practice/
├── files/
├── backup/
└── notes/
```

### Task

1.  Create the `linux-practice` directory.
2.  Enter it.
3.  Create the three directories inside it.
4.  Use `ls -la` to check the result.

------------------------------------------------------------------------

## Exercise 3 --- Create files

Inside the `files` directory create:

``` text
file1.txt
file2.txt
file3.txt
```

### Task

1.  Create all three files using one command.
2.  Check that they exist.
3.  Display the detailed information about them using `ls -l`.

------------------------------------------------------------------------

## Exercise 4 --- Copy files

Use the files from the previous exercise.

### Task

1.  Copy `file1.txt` into the `backup` directory.
2.  Copy `file2.txt` into the `backup` directory.
3.  Check the contents of `backup`.
4.  Copy the entire `files` directory into another directory called
    `files-copy`.

------------------------------------------------------------------------

## Exercise 5 --- Rename and move

### Task

1.  Rename `file3.txt` to `important.txt`.
2.  Move `important.txt` into the `notes` directory.
3.  Check that the file is no longer inside `files`.
4.  Check that it exists inside `notes`.

------------------------------------------------------------------------

## Exercise 6 --- Remove files

### Task

1.  Create a file called `temporary.txt`.
2.  Check that it exists.
3.  Remove it using `rm`.
4.  Check that it has been removed.

Then create:

``` text
old-files/
├── old1.txt
├── old2.txt
└── old3.txt
```

Remove the entire `old-files` directory.

------------------------------------------------------------------------

## Exercise 7 --- Absolute and relative paths

Assume you have this structure:

``` text
linux-practice/
├── files/
│   ├── file1.txt
│   └── file2.txt
├── backup/
└── notes/
```

### Task

From different directories:

1.  Navigate to `file1.txt` using a relative path.
2.  Navigate to `notes` using a relative path.
3.  Navigate to `linux-practice` using an absolute path.
4.  Return to your home directory using `~`.

------------------------------------------------------------------------

## Exercise 8 --- Reading files

Create a file called:

``` text
notes.txt
```

Put some text inside it.

For example:

``` text
Linux is an operating system kernel.
I am learning Linux for DevOps.
The terminal is one of the main tools I use.
```

### Task

1.  Display the entire file using `cat`.
2.  Display the file using `less`.
3.  Display the first line using `head`.
4.  Display the last line using `tail`.

------------------------------------------------------------------------

## Exercise 9 --- Help

### Task

Without searching the internet:

1.  Find the manual for `ls`.
2.  Find the manual for `mkdir`.
3.  Find the help information for `cp`.
4.  Find the help information for `rm`.

Use:

``` bash
man
```

and:

``` bash
--help
```

------------------------------------------------------------------------

## Exercise 10 --- Package management

This exercise is for Debian/Ubuntu systems.

### Task

1.  Update the package list.
2.  Check whether `curl` is installed.
3.  Install `curl` if it is not installed.
4.  Check the installed version.
5.  Remove `curl`.

Commands you may need:

``` bash
apt
```

and:

``` bash
curl --version
```

------------------------------------------------------------------------

## Exercise 11 --- Filesystem

Explore the basic Linux filesystem.

### Task

Check the contents of:

``` text
/
```

Then find and explore:

``` text
/home
/etc
/var
/tmp
/usr
/opt
/dev
/proc
```

For each directory, try to understand what kind of files or information
you can find there.

Use:

``` bash
ls
```

and:

``` bash
ls -la
```

------------------------------------------------------------------------

## Exercise 12 --- sudo

### Task

Try running:

``` bash
apt update
```

without `sudo`.

Then try:

``` bash
sudo apt update
```

### Goal

Understand why some commands require elevated privileges and why `sudo`
is used.

------------------------------------------------------------------------

# Final Exercise --- Linux Basics Challenge

Complete the following without looking at previous examples.

### Task

Create this structure:

``` text
linux-challenge/
├── documents/
│   ├── notes.txt
│   └── todo.txt
├── backup/
└── temporary/
```

Then:

1.  Navigate into `linux-challenge`.
2.  Create the required directories.
3.  Create both files inside `documents`.
4.  Add some text to `notes.txt`.
5.  Display the contents of `notes.txt`.
6.  Copy `notes.txt` into `backup`.
7.  Rename `todo.txt` to `tasks.txt`.
8.  Move `tasks.txt` into `backup`.
9.  Create a temporary file inside `temporary`.
10. Remove the temporary file.
11. Display the complete directory structure using `ls -la`.
12. Check your current location with `pwd`.
13. Go back to your home directory.

------------------------------------------------------------------------
