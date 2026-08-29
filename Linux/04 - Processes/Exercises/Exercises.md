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

- your shell ✅
  - `ps aux | grep SHELL` or `ps -p $$`
- the process using the most CPU ✅ 
  - `ps aux --sort=-%cpu`
- the process using the most memory ✅
  - `ps aux --sort=-%mem`
- PID 1 ✅
  - `ps -p 1`

Then display the processes in a different format.

```bash
htop
```

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

`htop`

Find:

1. The process using the most CPU. ✅
   1. `Click on CPU% tab`
2. The process using the most memory. ✅
   1. `Click on MEM% tab`
3. The PID of your shell. ✅
   1. `Click F4 - Add filter - Look for BASH`
4. The system load average. ✅
   1. `In htop there is Load Average: 0.85 0.82 0.64 above Uptime, those are values shown for 1min, 5min and 15min `

Repeat the exercise using an interactive process monitor if available.

```bash
top

- P → sort by **CPU usage**
- M → sort by **memory usage**
- 1 → show individual CPU cores
- q → quit
```

---

## Exercise 6 — Process Tree

Display the process hierarchy.

```bash
pstree    
```

Find:

- `systemd` ✅
  - `pstree | grep systemd`
- your terminal ✅
  - `├─ptyxis─┬─ptyxis-agent─┬─2*[bash]
     |        |              ├─bash─┬─htop
     |        │              │      ├─pstree
     |        │              │      └─top
     |        │              └─4*[{ptyxis-agent}]
     |        └─16*[{ptyxis}]`
- your shell ✅
  - `ps -p $$`
- a program started by your shell ✅
  - `bash─┬─htop
          ├─pstree
          └─top`

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

Start a process that runs for several minutes. ✅

```bash
  sleep 700 &
```

Find its PID. ✅

```bash
pgrep sleep
```

First, terminate it gracefully. ✅

```bash
kill 72154
```

Start another process and terminate it forcefully. ✅

```bash
 sleep 1000 & 

pgrep sleep

kill -9 72140
```

### Goal

Understand the difference between:

```text
SIGTERM
SIGKILL



kill sends SIGTERM, giving the process a chance to shut down slowly and clean up resources.

kill -9 sends SIGKILL, which terminates the process immediately without giving it a chance to clean up.
```

---

## Exercise 8 — Find a Process by Name

Start a process that runs for several minutes. ✅

```bash
sleep 300 &
```

Find the process by its name. ✅

`pgrep sleep`



Display its PID and command. ✅

`ps 72140` or `ps -p 72140 -o pid,cmd`



Then terminate it by name. ✅

`pkill sleep`



Verify that it is no longer running. ✅

`pgrep sleep`

### Goal

Learn how to find and manage processes by name.

---

## Exercise 9 — Process Priority

Start a CPU-intensive process with a lower priority. ✅

`nice -n 10 sleep 300 &`

Find the process and inspect its nice value. ✅

`pgrep sleep`

Change its priority while it is running. ✅

`renice 19 -p 72564`

Terminate the process when finished. ✅

`kill 72564`

### Goal

Understand the concept of **nice values** and process priority.

---

## Exercise 10 — Explore `/proc`

Find the PID of your shell. ✅

`ps aux | grep $$` or `echo $$`

Explore its directory inside `/proc`. ✅

`ls -l /proc/63698/cwd`

Find and inspect:

- process status ✅
  - `cat /proc/63698/status`
- command line ✅
  - `cat /proc/63698/cmdline`
- executable ✅
  - `ls -l /proc/63698/exe`
- current working directory ✅
  - `ls -l /proc/63698/cwd`
- environment variables ✅
  - `cat /proc/63698/environ`
- memory mappings ✅
  - `cat /proc/63698/maps`

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
