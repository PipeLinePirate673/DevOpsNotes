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

```bash
pgrep brave
```

Find all files and resources opened by that process.

Identify:

- regular files     ✅
  
  - `regular files will have REG (REG means a regular file)`

- shared libraries ✅
  
  - `shared libraries will have /usr/lib/.. or /lib/...`
  - `also shown as REG`

- terminal devices ✅
  
  - Terminal devices can be found under `/dev/pts/...``

- other resources ✅
  
  - `DIR` → directories
  - `CHR` → character devices
  - `FIFO` → pipes
  - `IPv4/IPv6` → network connections

### Goal

Understand that processes use files and other resources provided by the operating system.

---

## Exercise 12 — Network Processes

Display the network sockets currently listening on your system. ✅

```bash
ss -tulpn
```

Choose one listening service and identify: 

    Process - ZEN

- protocol ✅
  - `udp`
- port ✅
  - `:59285`
- PID ✅
  - `ss -tulpn | grep :59285`
    - `udp   UNCONN 0      0                              0.0.0.0:59285      0.0.0.0:*    users:(("zen",pid=67170,fd=203))   `
      - `PID=67170`
- process name ✅
  - `zen`

Then verify which process owns that port using another tool. ✅

`lsof -i :59285`

### Goal

Learn how to identify which process owns a network port.

---

## Exercise 13 — Find the Biggest CPU Consumer

Display the processes sorted by CPU usage. ✅

`ps aux --sort=-%cpu`

Identify the process using the most CPU.

   `dominik    21651 20.0  4.5 1526509360 701952 ?   Sl   21:37   6:39 /snap/brave/674/opt/brave.com/brave/brave --type=renderer --crashpad-handler-pid=10617 --enable-crash-reporter=a4d0f46e-16e1-40c7-b9a0-5ce8f95c5cac, --enable-distillabilit
d`



`ps -fp 21651`

Inspect its:

- PID  ✅
  - `21651`
- PPID ✅
  - `10630`
- user ✅
  - `dominik`
- CPU usage ✅
  - `20.0`
- memory usage ✅
  - `4.5`
- state ✅
  - `Sl`
- command ✅
  - `/snap/brave/674/opt/brave.com/brave/brave`

---

## Exercise 14 — Find the Biggest Memory Consumer

Display the processes sorted by memory usage.

`ps aux --sort=-%mem`

Identify the process using the most RAM.

`dominik    21651 11.4  5.3 1526509124 824624 ?   Sl   21:37   7:00 /snap/brave/674/opt/brave.com/brave/brave --type=renderer --crashpad-handler-pid=10617 --enable-crash-reporter=a4d0f46e-16e1-40c7-b9a0-5ce8f95c5cac, --enable-distillabilit
d`

Inspect its:

- PID ✅ 
  - `21651`
- PPID ✅ 
  - `10630`
- user ✅
  - `dominik`
- CPU usage ✅
  - `11.4`
- memory usage ✅
  - `5.3`
- state ✅
  - `Sl`
- command ✅
  - `/snap/brave/674/opt/brave.com/brave/brave`

---

## Exercise 15 — Troubleshooting Scenario

Imagine that a web application is not responding.
You know that it should be listening on port `8080`.
`lsof -i :8080`
Investigate the problem.

### Tasks

1. Check whether anything is listening on port `8080`. ✅
   1. `lsof -i :8080`
2. Identify the process. ✅
   1. `No process is listening on port 8080.`
3. Find its PID. ✅
   1. `No process is listening on port 8080.`
4. Check its CPU and memory usage. ✅
   1. `No process is listening on port 8080.`
5. Check its parent process. ✅
   1. `No process is listening on port 8080.`
6. Inspect its command line. ✅
   1. `No process is listening on port 8080.`
7. Inspect its open files. ✅
   1. `No process is listening on port 8080.`
8. If necessary, terminate the process. ✅
   1. `No process is listening on port 8080.`

---

# Challenge — Process Investigation

Choose any long-running process on your system.

Investigate it without using `htop`.

`ps aux`

`dominik    22076  1.1  1.7 1518734736 273628 ?   Sl   21:43   1:07 /opt/marktext/marktext`

`ps -fp 22076`



`dominik@Zenbook:~$ ps -l 22076
F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY        TIME CMD
4 S  1000   22076    5710  1  80   0 - 379684468 poll_s ?      1:11 /opt/marktext/marktext`



Find:

1. Process name
   1. `marktext`
2. PID
   1. `22076`
3. PPID
   1. `5710`
4. User
   1. `dominik`
5. Process state
   1. `Sl`
6. CPU usage
   1. `1.1`
7. Memory usage
   1. `1.7`
8. Nice value
   1. `0`
9. Executable path
   1. `/opt/marktext/marktext`
10. Working directory
    1. `ls -l /proc/22076/cwd`
       1. `lrwxrwxrwx 1 dominik dominik 0 Sep  1 23:29 /proc/22076/cwd -> /home/dominik`
11. Open files
    1. `lsof -p 22076`
12. Network connections
    1. `ss -nap | grep 22076 -i`
13. Parent process
    1. `ps -o ppid= -p 22076` or `ps -fp 5710` -  PID  | or `ps -o pid,ppid,cmd -p 22076`
14. Child processes
    1. `pstree -p 22076`

### Goal

Build the ability to investigate an unknown process using standard Linux tools.

---



# Final Challenge

Without looking at your notes, answer these questions:

1. What is a PID?
   1. `Process Identifier`
2. What is a PPID?
   1. `Parent process ID`
3. What is PID 1?
   1. `MAin procces -  systemd`
4. What is the difference between a process and a program?
   1. `A program is code stored on the system, while a process is a running instance of that program.`
5. What is the difference between foreground and background processes?
   1. `Background process let's you use terminal while foreground process block as long as it works`
6. What does `Ctrl + C` do?
   1. `Terminate/interrup Process`
7. What does `Ctrl + Z` do?
   1. `Suspend/Stops process`
8. What is the difference between `SIGTERM` and `SIGKILL`?
   1. `Sigterm is an signal which close process gently and give it time to save, sigkill kills process right away`
9. What does `ps aux` show?
   1. `All the processes that are running at that moment`
10. What is `top` used for?
    1. `Shows running processes and system resource usage in real time.`
11. What is `pstree` used for?
    1. `Shows all processes with their parent processes as tree`
12. What is `/proc`?
    1. `is a virtual filesystem that provides information about running processes and the Linux system`
13. What does `lsof` show?
    1. `Shows which files and other resources are opened by processes. It can also be used to find which process is using a network port`
14. What does `ss` show?
    1. `show network sockets and information about network connections and listening ports.`
15. What is a zombie process?
    1. `A zombie process is a process that has finished running but still has an entry in the process table`
16. What is an orphan process?
    1. `Is an process which parent have been killed but child process still works`
17. What is a nice value?
    1. `Nice value determines the priority of a process `
18. How would you find which process is using port `8080`?
    1. `lsof -i :8080`
19. How would you gracefully terminate PID `1234`?
    1. `kill 1234`
20. How would you forcefully terminate PID `1234`?
    1. `kill -9 1234`

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
