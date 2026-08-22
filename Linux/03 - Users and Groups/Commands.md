# Linux — Users & Groups Commands

## User Information

| Command | Purpose | Example |
|---|---|---|
| `whoami` | Show the current username | `whoami` |
| `id` | Show UID, GID and groups | `id` |
| `id username` | Show information about a specific user | `id dominik` |
| `groups` | Show groups of the current user | `groups` |
| `groups username` | Show groups of a specific user | `groups dominik` |
| `getent passwd username` | Query a specific user | `getent passwd dominik` |

---

## User Management

| Command | Purpose | Example |
|---|---|---|
| `sudo adduser username` | Create a user | `sudo adduser devuser` |
| `sudo useradd username` | Create a user using the low-level tool | `sudo useradd devuser` |
| `sudo useradd -m username` | Create a user with a home directory | `sudo useradd -m devuser` |
| `sudo useradd -m -s /bin/bash username` | Create a user with a home directory and Bash shell | `sudo useradd -m -s /bin/bash devuser` |
| `sudo deluser username` | Remove a user | `sudo deluser devuser` |
| `sudo deluser --remove-home username` | Remove a user and their home directory | `sudo deluser --remove-home devuser` |
| `sudo userdel username` | Remove a user | `sudo userdel devuser` |
| `sudo userdel -r username` | Remove a user and their home directory | `sudo userdel -r devuser` |

---

## Password Management

| Command | Purpose | Example |
|---|---|---|
| `passwd` | Change your own password | `passwd` |
| `sudo passwd username` | Change another user's password | `sudo passwd devuser` |
| `sudo passwd -l username` | Lock a user account | `sudo passwd -l devuser` |
| `sudo passwd -u username` | Unlock a user account | `sudo passwd -u devuser` |
| `sudo passwd -e username` | Force a password change at next login | `sudo passwd -e devuser` |
| `sudo passwd -S username` | Show password/account status | `sudo passwd -S devuser` |

---

## Group Management

| Command | Purpose | Example |
|---|---|---|
| `sudo groupadd groupname` | Create a group | `sudo groupadd developers` |
| `sudo groupdel groupname` | Delete a group | `sudo groupdel developers` |
| `getent group groupname` | Show information about a group | `getent group docker` |
| `getent group` | List groups from the system group database | `getent group` |
| `cat /etc/group` | Display the group file | `cat /etc/group` |

---

## Adding and Removing Group Membership

| Command | Purpose | Example |
|---|---|---|
| `sudo usermod -aG group username` | Add a user to a supplementary group | `sudo usermod -aG docker dominik` |
| `sudo deluser username group` | Remove a user from a group | `sudo deluser dominik docker` |
| `sudo gpasswd -a username group` | Add a user to a group | `sudo gpasswd -a dominik docker` |
| `sudo gpasswd -d username group` | Remove a user from a group | `sudo gpasswd -d dominik docker` |
| `newgrp groupname` | Start a shell with a new group as the current group | `newgrp docker` |

> **Important:** When using `usermod`, remember `-aG`. Without `-a`, you can accidentally replace the user's existing supplementary group memberships.

---

## `usermod`

| Command | Purpose | Example |
|---|---|---|
| `sudo usermod -aG group username` | Add supplementary group | `sudo usermod -aG docker dominik` |
| `sudo usermod -g group username` | Change primary group | `sudo usermod -g developers devuser` |
| `sudo usermod -s /bin/bash username` | Change login shell | `sudo usermod -s /bin/bash devuser` |
| `sudo usermod -d /home/newhome username` | Change home directory | `sudo usermod -d /home/newhome devuser` |
| `sudo usermod -d /home/newhome -m username` | Move the existing home directory | `sudo usermod -d /home/newhome -m devuser` |
| `sudo usermod -c "Full Name" username` | Change the user's comment/full name | `sudo usermod -c "Dev User" devuser` |
| `sudo usermod -L username` | Lock an account | `sudo usermod -L devuser` |
| `sudo usermod -U username` | Unlock an account | `sudo usermod -U devuser` |

---

## `sudo`

| Command | Purpose | Example |
|---|---|---|
| `sudo command` | Run a command with elevated privileges | `sudo apt update` |
| `sudo -i` | Open a root login shell | `sudo -i` |
| `sudo -u username command` | Run a command as another user | `sudo -u postgres psql` |
| `sudo -l` | Show your sudo permissions | `sudo -l` |
| `sudo visudo` | Safely edit the sudoers configuration | `sudo visudo` |

---

## `su`

| Command | Purpose | Example |
|---|---|---|
| `su - username` | Switch to another user | `su - devuser` |
| `su -` | Switch to root | `su -` |
| `su - username -c "command"` | Run one command as another user | `su - devuser -c "whoami"` |

---

## System User and Group Files

| Command | Purpose | Example |
|---|---|---|
| `cat /etc/passwd` | Display user account information | `cat /etc/passwd` |
| `getent passwd` | Query the system user database | `getent passwd` |
| `getent passwd username` | Query one user | `getent passwd dominik` |
| `cat /etc/shadow` | Display password hashes and password aging information | `sudo cat /etc/shadow` |
| `cat /etc/group` | Display group information | `cat /etc/group` |
| `getent group` | Query the system group database | `getent group` |

> **Security:** `/etc/shadow` contains sensitive authentication information. Avoid exposing its contents unnecessarily.

---

## Searching Users and Groups

| Command | Purpose | Example |
|---|---|---|
| `grep '^username:' /etc/passwd` | Find a specific user in `/etc/passwd` | `grep '^dominik:' /etc/passwd` |
| `sudo grep '^username:' /etc/shadow` | Find a specific user in `/etc/shadow` | `sudo grep '^dominik:' /etc/shadow` |
| `grep '^groupname:' /etc/group` | Find a specific group | `grep '^docker:' /etc/group` |
| `getent passwd username` | Check whether a user exists | `getent passwd devuser` |
| `getent group groupname` | Check whether a group exists | `getent group developers` |

---

## Logged-in Users

| Command | Purpose | Example |
|---|---|---|
| `who` | Show currently logged-in users | `who` |
| `w` | Show logged-in users and their activity | `w` |
| `users` | Show usernames currently logged in | `users` |
| `last` | Show login history | `last` |

---

## Shell Management

| Command | Purpose | Example |
|---|---|---|
| `echo $SHELL` | Show your current shell | `echo $SHELL` |
| `getent passwd username` | Show the user's configured shell | `getent passwd devuser` |
| `sudo usermod -s /bin/bash username` | Change the user's login shell | `sudo usermod -s /bin/bash devuser` |

Common shells:

```text
/bin/bash
/bin/zsh
/bin/sh
```

---

## Service Accounts

| Command | Purpose | Example |
|---|---|---|
| `id www-data` | Show information about a service account | `id www-data` |
| `getent passwd www-data` | Show service account configuration | `getent passwd www-data` |
| `getent passwd \| grep -E 'www-data\|postgres\|mysql\|nginx'` | Find common service accounts | `getent passwd \| grep -E 'www-data\|postgres\|mysql\|nginx'` |

---

# Quick Reference

| Task | Command |
|---|---|
| Show current user | `whoami` |
| Show user ID and groups | `id` |
| Show user's groups | `groups username` |
| Create user | `sudo adduser username` |
| Delete user | `sudo deluser username` |
| Change password | `passwd` |
| Create group | `sudo groupadd groupname` |
| Delete group | `sudo groupdel groupname` |
| Add user to group | `sudo usermod -aG group username` |
| Remove user from group | `sudo deluser username group` |
| Change primary group | `sudo usermod -g group username` |
| Lock user | `sudo usermod -L username` |
| Unlock user | `sudo usermod -U username` |
| Run command as root | `sudo command` |
| Open root shell | `sudo -i` |
| Run command as another user | `sudo -u username command` |
| Switch user | `su - username` |
| Check sudo permissions | `sudo -l` |
| Edit sudoers safely | `sudo visudo` |
| List users | `getent passwd` |
| List groups | `getent group` |
| Check if user exists | `id username` |
| Check if group exists | `getent group groupname` |
| Show logged-in users | `who` |
| Show login activity | `w` |
| Show login history | `last` |

---

# Commands Worth Memorizing

For everyday Linux administration, focus on these first:

```bash
whoami
id
groups
sudo
sudo -i
sudo -u
adduser
deluser
passwd
groupadd
usermod -aG
getent passwd
getent group
who
w
visudo
```

The most important pattern for group management:

```bash
sudo usermod -aG group username
```

The most useful command for inspecting a user:

```bash
id username
```
