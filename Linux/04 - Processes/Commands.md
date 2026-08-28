# Linux — Processes Commands

## Process Information

| Command | Purpose | Example |
|---|---|---|
| `ps` | Show processes for the current shell | `ps` |
| `ps aux` | Show all running processes with detailed information | `ps aux` |
| `ps -ef` | Show all processes in full format | `ps -ef` |
| `ps -p PID` | Show a specific process | `ps -p 1234` |
| `ps -fp PID` | Show detailed information about a specific process | `ps -fp 1234` |
| `echo $$` | Show the PID of the current shell | `echo $$` |
| `pgrep process_name` | Find a process by name | `pgrep nginx` |
| `pgrep -a process_name` | Find a process and show its command | `pgrep -a nginx` |

---

## Process Monitoring

| Command | Purpose | Example |
|---|---|---|
| `top` | Monitor processes in real time | `top` |
| `htop` | Interactive process monitor | `htop` |
| `pstree` | Show the process hierarchy | `pstree` |
| `pstree -p` | Show the process hierarchy with PIDs | `pstree -p` |
| `ps aux --sort=-%cpu` | Sort processes by CPU usage | `ps aux --sort=-%cpu` |
| `ps aux --sort=-%mem` | Sort processes by memory usage | `ps aux --sort=-%mem` |
| `watch "ps aux"` | Continuously monitor the process list | `watch "ps aux"` |

---

## Background & Foreground Processes

| Command | Purpose | Example |
|---|---|---|
| `command &` | Start a command in the background | `sleep 300 &` |
| `jobs` | Show background jobs started by the current shell | `jobs` |
| `fg` | Bring the last background job to the foreground | `fg` |
| `fg %1` | Bring a specific job to the foreground | `fg %1` |
| `bg` | Resume a stopped job in the background | `bg` |
| `bg %1` | Resume a specific stopped job in the background | `bg %1` |
| `Ctrl + C` | Interrupt a foreground process | `Ctrl + C` |
| `Ctrl + Z` | Suspend a foreground process | `Ctrl + Z` |

---

## Process Signals

| Command | Purpose | Example |
|---|---|---|
| `kill PID` | Send SIGTERM to a process | `kill 1234` |
| `kill -15 PID` | Send SIGTERM explicitly | `kill -15 1234` |
| `kill -SIGTERM PID` | Send SIGTERM by name | `kill -SIGTERM 1234` |
| `kill -9 PID` | Force-kill a process with SIGKILL | `kill -9 1234` |
| `kill -SIGKILL PID` | Send SIGKILL explicitly | `kill -SIGKILL 1234` |
| `pkill process_name` | Send a signal to processes by name | `pkill nginx` |
| `killall process_name` | Kill processes by name | `killall nginx` |
| `kill -l` | List available signals | `kill -l` |

---

## Process Priority

| Command | Purpose | Example |
|---|---|---|
| `nice -n VALUE command` | Start a process with a specific nice value | `nice -n 10 backup.sh` |
| `renice VALUE -p PID` | Change the nice value of a running process | `renice 10 -p 1234` |

---

## Process Files & Resources

| Command | Purpose | Example |
|---|---|---|
| `lsof -p PID` | Show files opened by a process | `lsof -p 1234` |
| `lsof /path/to/file` | Show which process is using a file | `lsof /var/log/app.log` |
| `cat /proc/PID/status` | Show detailed process information | `cat /proc/1234/status` |
| `cat /proc/PID/cmdline` | Show the command used to start a process | `cat /proc/1234/cmdline` |
| `ls -l /proc/PID/exe` | Show the executable used by a process | `ls -l /proc/1234/exe` |
| `ls -l /proc/PID/cwd` | Show the current working directory of a process | `ls -l /proc/1234/cwd` |
| `cat /proc/PID/environ` | Show environment variables of a process | `cat /proc/1234/environ` |
| `cat /proc/PID/maps` | Show memory mappings of a process | `cat /proc/1234/maps` |

---

## Network Processes

| Command | Purpose | Example |
|---|---|---|
| `ss -tulpn` | Show listening TCP/UDP sockets and processes | `sudo ss -tulpn` |
| `ss -tulpn \| grep :PORT` | Find a process listening on a specific port | `sudo ss -tulpn \| grep :8080` |
| `lsof -i :PORT` | Find processes using a specific port | `sudo lsof -i :8080` |

---

## Common Process Troubleshooting

| Command | Purpose | Example |
|---|---|---|
| `pgrep nginx` | Check if nginx is running | `pgrep nginx` |
| `ps -fp $(pgrep nginx)` | Show details about nginx | `ps -fp $(pgrep nginx)` |
| `sudo ss -tulpn` | Check which services are listening on ports | `sudo ss -tulpn` |
| `ps aux --sort=-%cpu` | Find processes using the most CPU | `ps aux --sort=-%cpu` |
| `ps aux --sort=-%mem` | Find processes using the most RAM | `ps aux --sort=-%mem` |
| `sudo lsof -i :8080` | Find what is using port 8080 | `sudo lsof -i :8080` |
| `pstree -p` | Understand parent/child processes | `pstree -p` |

---

## Quick Reference

| Command | Purpose |
|---|---|
| `ps aux` | List all processes |
| `ps -ef` | List processes with PPID |
| `top` | Monitor processes |
| `htop` | Interactive process monitor |
| `pgrep` | Find processes |
| `pkill` | Signal processes by name |
| `kill` | Signal a process by PID |
| `killall` | Kill processes by name |
| `jobs` | Show shell jobs |
| `fg` | Move a job to foreground |
| `bg` | Move a job to background |
| `pstree` | Show process hierarchy |
| `nice` | Start a process with a priority |
| `renice` | Change process priority |
| `lsof` | Show open files/resources |
| `ss` | Show network sockets |
| `/proc/PID/` | Kernel information about a process |
