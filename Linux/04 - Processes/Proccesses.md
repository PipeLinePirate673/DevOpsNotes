# Linux Processes

A **process** is a running instance of a program.

Whenever you run a program, Linux creates a process to execute it.

Examples:

- `bash` / `zsh` — a shell process
- `docker` — a Docker process
- `nginx` — a web server process
- `python app.py` — a Python process
- `ssh` — an SSH process
- `systemd` — the main system management process

Every process has its own:

- PID
- parent process
- owner
- state
- CPU usage
- memory usage
- priority
- open files
- network connections

---

# 1. PID

**PID** stands for:

> Process ID

Every running process has a unique process ID.

You can see the PID of your current shell with:

```bash
echo $$
```

Example:

```text
2841
```

You can also find a process PID using:

```bash
pgrep process_name
```

Example:

```bash
pgrep nginx
```

---

# 2. PPID

**PPID** stands for:

> Parent Process ID

Processes are usually created by other processes.

For example:

```text
systemd
   │
   └── bash
        │
        └── python
```

Here:

- `systemd` is the parent of `bash`
- `bash` is the parent of `python`

You can see PID and PPID with:

```bash
ps -ef
```

Example:

```text
UID        PID   PPID  C STIME TTY          TIME CMD
dominik   2841   1800  0 22:10 pts/0    00:00:00 bash
dominik   3920   2841  0 22:15 pts/0    00:00:01 python app.py
```

The Python process:

```text
PID  = 3920
PPID = 2841
```

So `bash` started the Python process.

---

# 3. PID 1

On most modern Linux distributions, the first userspace process is:

```text
systemd
```

It normally has:

```text
PID 1
```

You can check it:

```bash
ps -p 1
```

Example:

```text
PID TTY          TIME CMD
1   ?        00:00:03 systemd
```

`systemd` is responsible for managing many parts of the system, including:

- system services
- processes
- boot sequence
- service dependencies
- service startup and shutdown

---

# 4. Process States

A process can be in different states.

Common states include:

| State | Meaning |
|---|---|
| `R` | Running |
| `S` | Sleeping |
| `D` | Uninterruptible sleep |
| `T` | Stopped |
| `Z` | Zombie |

You can see the process state with:

```bash
ps aux
```

Look at the `STAT` column.

Example:

```text
USER       PID %CPU %MEM STAT COMMAND
dominik   3920  1.2  2.1 S    python app.py
```

The `S` means the process is sleeping.

---

# 5. Foreground Processes

When you run:

```bash
sleep 100
```

the process runs in the **foreground**.

Your terminal is occupied by the process.

You cannot normally use that terminal to enter other commands until the process finishes.

---

# 6. Background Processes

You can start a process in the background by adding:

```bash
&
```

Example:

```bash
sleep 100 &
```

You might see:

```text
[1] 4210
```

Where:

```text
[1]    Job ID
4210   PID
```

You can continue using the terminal while `sleep` runs.

---

# 7. jobs

The `jobs` command shows background jobs started from the current shell.

```bash
jobs
```

Example:

```text
[1]+  Running    sleep 100 &
```

The number `[1]` is the job ID.

---

# 8. fg

`fg` brings a background job into the foreground.

```bash
fg
```

For a specific job:

```bash
fg %1
```

Here `%1` refers to job number `1`.

---

# 9. bg

If a process is stopped with:

```text
Ctrl + Z
```

you can resume it in the background:

```bash
bg
```

Example:

```bash
sleep 100
```

Press:

```text
Ctrl + Z
```

Then:

```bash
bg
```

The process will continue running in the background.

---

# 10. Ctrl + C

Pressing:

```text
Ctrl + C
```

sends the process:

```text
SIGINT
```

**SIGINT** means:

> Interrupt

It normally asks the process to stop.

Example:

```bash
ping google.com
```

Press:

```text
Ctrl + C
```

The `ping` process will normally terminate.

---

# 11. Ctrl + Z

Pressing:

```text
Ctrl + Z
```

sends:

```text
SIGTSTP
```

The process is **stopped**, not terminated.

You can later resume it with:

```bash
fg
```

or:

```bash
bg
```

---

# 12. ps

`ps` stands for:

> Process Status

The simplest command:

```bash
ps
```

shows processes associated with the current terminal.

A more useful command is:

```bash
ps aux
```

This shows processes from all users.

Example:

```text
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1  17000 11000 ?        Ss   21:00   0:03 /sbin/init
dominik   2841  0.1  0.5  25000 18000 pts/0    Ss   22:10   0:00 bash
dominik   3920  1.2  2.1 120000 50000 pts/0    S    22:15   0:03 python app.py
```

Important columns:

| Column | Meaning |
|---|---|
| `USER` | Process owner |
| `PID` | Process ID |
| `%CPU` | CPU usage |
| `%MEM` | Memory usage |
| `VSZ` | Virtual memory size |
| `RSS` | Physical RAM used |
| `TTY` | Terminal |
| `STAT` | Process state |
| `START` | Start time |
| `TIME` | CPU time used |
| `COMMAND` | Command that started the process |

---

# 13. ps -ef

Another very common format is:

```bash
ps -ef
```

Example:

```text
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 21:00 ?        00:00:03 systemd
dominik   2841  1800  0 22:10 pts/0    00:00:00 bash
dominik   3920  2841  1 22:15 pts/0    00:00:03 python app.py
```

`ps -ef` is especially useful when you want to understand parent-child relationships.

---

# 14. top

`top` displays running processes in real time.

Run:

```bash
top
```

It shows information such as:

- CPU usage
- RAM usage
- load average
- running processes
- process IDs
- process states

Press:

```text
q
```

to quit.

---

# 15. htop

`htop` is a more user-friendly alternative to `top`.

Install it on Debian/Ubuntu:

```bash
sudo apt install htop
```

Run:

```bash
htop
```

It allows you to:

- sort processes
- search for processes
- view CPU usage
- view RAM usage
- kill processes
- inspect process trees

---

# 16. Finding a Process

You can use `pgrep`:

```bash
pgrep nginx
```

Or:

```bash
pgrep -a nginx
```

The `-a` option also displays the command.

Another common approach is:

```bash
ps aux | grep nginx
```

However, `pgrep` is usually cleaner when you simply want to find a process.

---

# 17. Killing Processes

The `kill` command sends a signal to a process.

Example:

```bash
kill 3920
```

By default, `kill` sends:

```text
SIGTERM
```

---

# 18. SIGTERM

`SIGTERM` means:

> Terminate

It asks a process to terminate gracefully.

A process can handle SIGTERM and perform cleanup before exiting.

For example, a server may:

1. stop accepting new connections
2. finish existing requests
3. close files
4. close network connections
5. exit

Because of this, **SIGTERM should normally be your first choice when stopping a process**.

---

# 19. SIGKILL

You can forcefully terminate a process with:

```bash
kill -9 PID
```

For example:

```bash
kill -9 3920
```

Signal `9` is:

```text
SIGKILL
```

Unlike SIGTERM, a process cannot catch or ignore SIGKILL.

Use it carefully.

A good general approach is:

```bash
kill PID
```

and only if the process refuses to terminate:

```bash
kill -9 PID
```

---

# 20. Listing Signals

You can list available signals with:

```bash
kill -l
```

Common signals:

| Signal | Number | Purpose |
|---|---:|---|
| `SIGHUP` | 1 | Hangup |
| `SIGINT` | 2 | Interrupt |
| `SIGQUIT` | 3 | Quit |
| `SIGKILL` | 9 | Force termination |
| `SIGTERM` | 15 | Graceful termination |
| `SIGSTOP` | 19 | Stop process |
| `SIGCONT` | 18 | Continue stopped process |

---

# 21. Sending a Specific Signal

You can specify the signal explicitly:

```bash
kill -SIGTERM 3920
```

or:

```bash
kill -15 3920
```

These are equivalent.

For SIGKILL:

```bash
kill -SIGKILL 3920
```

or:

```bash
kill -9 3920
```

---

# 22. killall

`killall` can terminate processes by name instead of PID.

Example:

```bash
killall firefox
```

This can terminate all matching `firefox` processes.

Be careful when using it.

---

# 23. Process Priority

Linux processes have a priority value called:

**nice value**

The nice value ranges from:

```text
-20
```

to:

```text
19
```

General rule:

```text
-20  → higher priority
  0  → default
 19  → lower priority
```

A process with a higher nice value is being "nicer" to other processes and receives less CPU priority.

---

# 24. nice

You can start a process with a specific nice value:

```bash
nice -n 10 command
```

Example:

```bash
nice -n 10 ./backup.sh
```

This gives the backup process a lower CPU priority.

This can be useful for background tasks such as:

- backups
- compression
- large file processing
- batch jobs

---

# 25. renice

You can change the nice value of an already running process.

Example:

```bash
renice 10 -p 3920
```

This changes the nice value of PID `3920` to `10`.

Changing priority to a higher priority usually requires elevated privileges.

For example:

```bash
sudo renice -10 -p 3920
```

---

# 26. Process Tree

You can visualize parent-child relationships with:

```bash
pstree
```

Example:

```text
systemd
├─ NetworkManager
├─ sshd
│  └─ sshd
│     └─ bash
│        └─ python
└─ docker
```

This is useful for understanding how processes are related.

You can also show PIDs:

```bash
pstree -p
```

Example:

```text
systemd(1)
 ├─sshd(1200)
 │  └─bash(2841)
 │     └─python(3920)
 └─docker(1500)
```

---

# 27. Zombie Processes

A **zombie process** is a process that has already finished execution but still has an entry in the process table.

It happens when:

1. a child process finishes
2. the parent has not yet collected its exit status

A zombie normally appears with:

```text
Z
```

in the process state.

You can search for zombies:

```bash
ps aux | grep ' Z '
```

Or inspect the process tree:

```bash
pstree -p
```

A single zombie is usually not a problem.

A large number of zombies can indicate a problem with a parent process.

---

# 28. Orphan Processes

An **orphan process** is a process whose parent has terminated.

Linux re-parents orphaned processes to another process, traditionally PID 1.

Example:

```text
bash
 └── python
```

If `bash` terminates while Python is still running:

```text
systemd
 └── python
```

The process is adopted by the system's init process.

---

# 29. /proc

Linux exposes information about running processes through:

```text
/proc
```

Each process normally has its own directory:

```text
/proc/PID
```

For example:

```text
/proc/3920
```

You can inspect it:

```bash
ls /proc/3920
```

You can see the command line used to start the process:

```bash
cat /proc/3920/cmdline
```

You can inspect process status:

```bash
cat /proc/3920/status
```

You can inspect the process executable:

```bash
ls -l /proc/3920/exe
```

`/proc` is a **virtual filesystem** provided by the Linux kernel.

---

# 30. Open Files

Linux treats many resources as files.

You can use:

```bash
lsof
```

to see files opened by processes.

For a specific process:

```bash
lsof -p 3920
```

You can also find which process is using a particular file:

```bash
lsof /path/to/file
```

This is extremely useful when troubleshooting services.

---

# 31. Network Connections

`ss` can show network sockets and connections.

Example:

```bash
ss -tulpn
```

This can help you identify:

- listening ports
- TCP connections
- UDP sockets
- processes using network ports

Example:

```text
tcp   LISTEN   0   128   0.0.0.0:80   0.0.0.0:*   users:(("nginx",pid=1500))
```

This tells you that `nginx` is listening on port `80`.

---

# 32. Useful Process Commands

| Command | Purpose |
|---|---|
| `ps` | Show processes |
| `ps aux` | Show detailed process list |
| `ps -ef` | Show processes with PPID |
| `top` | Monitor processes |
| `htop` | Interactive process monitor |
| `pgrep` | Find processes by name |
| `pkill` | Send signals to processes by name |
| `kill` | Send a signal to a PID |
| `killall` | Kill processes by name |
| `jobs` | Show shell jobs |
| `fg` | Bring a job to foreground |
| `bg` | Resume a job in background |
| `pstree` | Show process hierarchy |
| `nice` | Start a process with a nice value |
| `renice` | Change process priority |
| `lsof` | Show open files |
| `ss` | Show network sockets |

---

# 33. Practical Examples

## Find a process

```bash
pgrep nginx
```

## Find detailed information

```bash
ps -fp $(pgrep nginx)
```

## Monitor processes

```bash
top
```

## Find the process using a port

```bash
sudo ss -tulpn
```

## Stop a process gracefully

```bash
kill PID
```

## Force a process to stop

```bash
kill -9 PID
```

## Start a command in the background

```bash
command &
```

## View background jobs

```bash
jobs
```

## Bring a job to foreground

```bash
fg %1
```

## Resume a stopped job

```bash
bg %1
```

## View process hierarchy

```bash
pstree -p
```

---

# 34. Important DevOps Concepts

Understanding processes is extremely important in DevOps.

When troubleshooting a server, you often need to answer questions like:

### Is the service running?

```bash
ps aux | grep nginx
```

### What is consuming CPU?

```bash
top
```

### What is consuming RAM?

```bash
top
```

Then sort by memory usage.

In `top`, press:

```text
M
```

### What process is listening on port 8080?

```bash
sudo ss -tulpn | grep :8080
```

### Which process owns a file?

```bash
sudo lsof /path/to/file
```

### Who started this process?

```bash
ps -ef
```

Look at:

```text
PID
PPID
```

### Why won't a process stop?

First:

```bash
kill PID
```

Check it:

```bash
ps -p PID
```

If it still exists:

```bash
kill -9 PID
```

---

# 35. Process Management Mental Model

A useful way to think about Linux processes:

```text
Program
   │
   │ executed
   ▼
Process
   │
   ├── PID
   ├── PPID
   ├── Owner
   ├── State
   ├── CPU usage
   ├── Memory usage
   ├── Open files
   └── Network connections
```

Processes form a hierarchy:

```text
systemd (PID 1)
│
├── sshd
│   └── bash
│       ├── vim
│       └── python
│
├── docker
│   ├── container process
│   └── container process
│
└── nginx
    ├── worker
    └── worker
```

This hierarchy is fundamental to understanding Linux.

---

# 36. Practice Exercises

## Exercise 1 — Find Your Shell

Find the PID of your current shell:

```bash
echo $$
```

Then verify it:

```bash
ps -p $$
```

---

## Exercise 2 — Background Process

Start:

```bash
sleep 300 &
```

Check your jobs:

```bash
jobs
```

Find the process:

```bash
pgrep sleep
```

Then terminate it:

```bash
kill PID
```

---

## Exercise 3 — Foreground and Background

Run:

```bash
sleep 300
```

Press:

```text
Ctrl + Z
```

Check:

```bash
jobs
```

Resume it in the background:

```bash
bg
```

Bring it back:

```bash
fg
```

Terminate it:

```text
Ctrl + C
```

---

## Exercise 4 — Process Tree

Run:

```bash
pstree -p
```

Find:

- PID 1
- your shell
- your terminal
- any programs you started

Try to understand their parent-child relationships.

---

## Exercise 5 — Find a Network Process

Run:

```bash
sudo ss -tulpn
```

Find a service listening on your machine.

Identify:

- port
- protocol
- PID
- process name

---

## Exercise 6 — CPU Usage

Run:

```bash
top
```

Find the process using the most CPU.

Then identify it using:

```bash
ps -fp PID
```

---

# 37. Quick Cheat Sheet

```bash
# Current shell PID
echo $$

# Show processes
ps

# Detailed process list
ps aux

# Show PID + PPID
ps -ef

# Find process
pgrep nginx

# Interactive process monitor
top

# Better interactive monitor
htop

# Process tree
pstree -p

# Start in background
command &

# Show shell jobs
jobs

# Bring job to foreground
fg %1

# Resume stopped job in background
bg %1

# Send SIGTERM
kill PID

# Send SIGKILL
kill -9 PID

# List signals
kill -l

# Start with lower priority
nice -n 10 command

# Change priority
renice 10 -p PID

# Open files
lsof -p PID

# Network sockets
ss -tulpn

# Process information
cat /proc/PID/status
```

---

# Key Takeaways

- A **process** is a running instance of a program.
- Every process has a **PID**.
- Most processes have a **parent process**, identified by **PPID**.
- **PID 1** is normally `systemd` on modern Linux systems.
- `ps` is used to inspect processes.
- `top` and `htop` are used to monitor processes.
- `kill` sends signals to processes.
- `SIGTERM` (`15`) asks a process to terminate gracefully.
- `SIGKILL` (`9`) forcefully terminates a process.
- `Ctrl + C` sends `SIGINT`.
- `Ctrl + Z` stops a foreground process.
- `bg` resumes a stopped process in the background.
- `fg` brings a background job to the foreground.
- `pstree` helps visualize process relationships.
- `/proc` exposes kernel information about processes.
- `lsof` shows resources opened by processes.
- `ss` helps identify processes using network sockets.
- Understanding processes is essential for Linux administration and DevOps.
