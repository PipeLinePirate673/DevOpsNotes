# Linux — Processes Exercises

## Exercise 1 — Find Your Shell Process

1. Find the PID of your current shell. ✅
   1. `echo $$`
2. Verify the PID. ✅
   1. `ps -p 19758`
3. Find the parent PID of your shell. ✅
   1. `ps -ef | grep 19758`  or `ps -fp 19758`

### Goal

Understand the difference between **PID** and **PPID**.

---

## Exercise 2 — Start a Background Process

Start a process that runs for 5 minutes. ✅

Then:

1. Check the background jobs. ✅
   1. `jobs`
2. Find the PID of the process. ✅ 
   1. `jobs -l`
3. Display detailed information about it. ✅
   1. `ps -fp 29996`
4. Terminate the process. ✅
   1. `kill 29996`

---

## Exercise 3 — Foreground vs Background

Start a process that runs for several minutes. ✅

```bash
sleep 700
```

Then:

1. Suspend the process. ✅
   1. `CTRL + Z`
2. Check its state. ✅ 
   1. `jobs -l` 
      1. `[5]+ 30550 Zatrzymany                 sleep 701` - 'Zatrzymany' - Stopped in Polish
3. Resume it in the background. ✅
   1. `bg`
4. Bring it back to the foreground. ✅
   1. `fg %5`
5. Terminate it. ✅
   1. `kill 30550`

### Goal

Understand the difference between **foreground** and **background** processes.

---

## Exercise 4 — Explore `ps`

Display the running processes on your system.

Find:

- your shell
- the process using the most CPU
- the process using the most memory
- PID 1

Then display the processes in a different format.

### Goal

Learn how to read:

- PID
- PPID
- CPU usage
- memory usage
- process state
- command

---

## Exercise 5 — Monitor Processes

Use a real-time process monitor.

Find:

1. The process using the most CPU.
2. The process using the most memory.
3. The PID of your shell.
4. The system load average.

Repeat the exercise using an interactive process monitor if available.

---

## Exercise 6 — Process Tree

Display the process hierarchy.

Find:

- `systemd`
- your terminal
- your shell
- a program started by your shell

Draw the relationship:

```text
Parent
  └── Child
       └── Child
```

### Goal

Understand parent-child process relationships.

---

## Exercise 7 — Process Signals

Start a process that runs for several minutes.

Find its PID.

First, terminate it gracefully.

Start another process and terminate it forcefully.

### Goal

Understand the difference between:

```text
SIGTERM
SIGKILL
```

---

## Exercise 8 — Find a Process by Name

Start a process that runs for several minutes.

Find the process by its name.

Display its PID and command.

Then terminate it by name.

Verify that it is no longer running.

### Goal

Learn how to find and manage processes by name.

---

## Exercise 9 — Process Priority

Start a CPU-intensive process with a lower priority.

Find the process and inspect its nice value.

Change its priority while it is running.

Terminate the process when finished.

### Goal

Understand the concept of **nice values** and process priority.

---

## Exercise 10 — Explore `/proc`

Find the PID of your shell.

Explore its directory inside `/proc`.

Find and inspect:

- process status
- command line
- executable
- current working directory
- environment variables
- memory mappings

### Goal

Understand how Linux exposes process information through `/proc`.

---

## Exercise 11 — Open Files

Choose a running process.

Find all files and resources opened by that process.

Identify:

- regular files
- shared libraries
- terminal devices
- other resources

### Goal

Understand that processes use files and other resources provided by the operating system.

---

## Exercise 12 — Network Processes

Display the network sockets currently listening on your system.

Choose one listening service and identify:

- protocol
- port
- PID
- process name

Then verify which process owns that port using another tool.

### Goal

Learn how to identify which process owns a network port.

---

## Exercise 13 — Find the Biggest CPU Consumer

Display the processes sorted by CPU usage.

Identify the process using the most CPU.

Inspect its:

- PID
- PPID
- user
- CPU usage
- memory usage
- state
- command

---

## Exercise 14 — Find the Biggest Memory Consumer

Display the processes sorted by memory usage.

Identify the process using the most RAM.

Inspect its:

- PID
- PPID
- user
- CPU usage
- memory usage
- state
- command

---

## Exercise 15 — Troubleshooting Scenario

Imagine that a web application is not responding.

You know that it should be listening on port `8080`.

Investigate the problem.

### Tasks

1. Check whether anything is listening on port `8080`.
2. Identify the process.
3. Find its PID.
4. Check its CPU and memory usage.
5. Check its parent process.
6. Inspect its command line.
7. Inspect its open files.
8. If necessary, terminate the process.

---

# Challenge — Process Investigation

Choose any long-running process on your system.

Investigate it without using `htop`.

Find:

1. Process name
2. PID
3. PPID
4. User
5. Process state
6. CPU usage
7. Memory usage
8. Nice value
9. Executable path
10. Working directory
11. Open files
12. Network connections
13. Parent process
14. Child processes

### Goal

Build the ability to investigate an unknown process using standard Linux tools.

---

# Mini Project — Process Monitor

Create a simple Bash script called:

```text
process-monitor.sh
```

The script should display:

- current date and time
- hostname
- current user
- system load
- top 5 CPU-consuming processes
- top 5 memory-consuming processes

Example output:

```text
========================================
        Linux Process Monitor
========================================

Date:
Hostname:
User:

Load Average:
...

Top CPU Processes:
...

Top Memory Processes:
...

========================================
```

### Requirements

- The script must be written in Bash.
- Do not use `htop`.
- Make the output easy to read.
- Use standard Linux utilities.

### Bonus

Add an optional PID argument.

When a PID is provided, the script should display detailed information about that process.

Example:

```text
./process-monitor.sh PID
```

---

# Final Challenge

Without looking at your notes, answer these questions:

1. What is a PID?
2. What is a PPID?
3. What is PID 1?
4. What is the difference between a process and a program?
5. What is the difference between foreground and background processes?
6. What does `Ctrl + C` do?
7. What does `Ctrl + Z` do?
8. What is the difference between `SIGTERM` and `SIGKILL`?
9. What does `ps aux` show?
10. What is `top` used for?
11. What is `pstree` used for?
12. What is `/proc`?
13. What does `lsof` show?
14. What does `ss` show?
15. What is a zombie process?
16. What is an orphan process?
17. What is a nice value?
18. How would you find which process is using port `8080`?
19. How would you gracefully terminate PID `1234`?
20. How would you forcefully terminate PID `1234`?

---

# Practical Goal

After completing these exercises, you should be comfortable with:

```text
Find a process
      ↓
Inspect a process
      ↓
Understand its parent
      ↓
Monitor its resources
      ↓
Find its files/network connections
      ↓
Send signals
      ↓
Terminate or troubleshoot it
```
