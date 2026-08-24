# Linux — Users & Groups Exercises

---

## Exercise 1 — Identify Yourself ✅

Find out:

- your username,
- your UID,
- your primary GID,
- your primary group,
- all supplementary groups,
- your current shell.

### Tasks

1. Find your username. ✅
   1. `whoami`
2. Find your UID and GID. ✅
   1. `id`
3. Find all groups you belong to. ✅
   1. `groups dominik`
4. Find your current shell. ✅
   1. `echo $SHELL`

---

## Exercise 2 — Inspect Your User ✅

Use the system user database to inspect your account.

### Tasks

Find your:

- username ✅
  - `whoami`
- UID ✅
  - `id` or `id | grep uid`
- GID ✅
  - `id` od `id | grep gid`
- home directory ✅
  - `pwd`
- login shell ✅
  - `echo $SHELL`

---

## Exercise 3 — Create a User ✅

Create a new user called:

```text
devuser
```

### Tasks

1. Create the user. ✅
   1. `sudo adduser devuser`
2. Check whether the user exists. ✅
   1. `getent passwd devuser`
3. Display the user's UID and GID. ✅
   1. `id devuser`
4. Display the user's home directory and shell. ✅
   1. `getent passwd devuser`

---

## Exercise 4 — Create a Development Group ✅

Create a group called:

```text
developers
```

### Tasks

1. Create the group. ✅
   1. `sudo groupadd developers`
2. Verify that it exists. ✅
   1. `getent group | grep developers`
3. Display information about the group. ✅
   1. `getent group developers`

---

## Exercise 5 — Add a User to a Group ✅

Add:

```text
devuser
```

to:

```text
developers
```

### Tasks

1. Add the user to the group. ✅
   1. `sudo gpasswd -a devuser developers`
2. Verify the membership. ✅
   1. `getent group developers`
3. Check the user's groups using both `groups` and `id`. ✅
   1. `groups devuser; id devuser`

### 

---

## Exercise 6 — Create Multiple Groups ✅

Create these groups:

```text
developers
dockerusers
backupusers
```

### Tasks

1. Create all three groups.  ✅
   1. `sudo groupadd dockerusers; sudo groupadd backupusers`
2. Add `devuser` to: 
   - `developers` ✅
     - `sudo gpasswd -a devuser developers`
   - `dockerusers` ✅
     - `sudo gpasswd -a devuser dockerusers`
3. Do **not** add `devuser` to `backupusers`. ✅
4. Verify the final group membership. ✅
   1. `groups devuser`

### Goal

You should end up with something similar to:

```text
devuser
├── primary group
├── developers
└── dockerusers
```

---

## Exercise 7 — Remove a User from a Group ✅

Remove `devuser` from:

```text
dockerusers
```

### Tasks

1. Remove the user from the group. ✅
   1. `sudo deluser devuser dockerusers`
2. Verify that the membership is gone. ✅
   1. `groups devuser`
3. Make sure `devuser` is still a member of `developers`. ✅
   1. `groups devuser`

---

## Exercise 8 — Primary vs Supplementary Groups ✅

Use `id` to investigate the difference between:

- primary group,
- supplementary groups.

### Tasks

1. Check the primary GID of `devuser`. ✅
   1. `id devuser`
2. Check the supplementary groups. 
   1. `id devuser`
3. Explain the difference in your own words.
   1. `The primary group is the main group for a user. A user can have only one primary group. Supplementary groups are additional groups that a user can belong to. A user can belong to multiple supplementary groups and get additional permissions from them.`

### Expected format

Write your answer in your notes:

```text
UID: 1001(devuser)
Primary GID: 1001(devuser)
Primary group: 1001(devuser)
Supplementary groups: 100(users), 1002(developers), 1003(dockerusers)
```

---

## Exercise 9 — Change the Primary Group ✅

Make:

```text
developers
```

the primary group of:

```text
devuser
```

### Tasks

1. Change the primary group. ✅
   1. `sudo usermod -g developers devuser`
2. Verify the result. ✅
   1. `id devuser`
      1. `uid=1001(devuser) gid=1002(developers) groups=1002(developers),100(users), 1003(dockerusers)`
3. Check whether the user still belongs to their supplementary groups. ✅
   1. `groups devuser`

### 

---

## Exercise 10 — Password Management ✅

Practice password management with `devuser`.

### Tasks

1. Set a password for `devuser`. ✅
   1. `sudo passwd devuser`
2. Lock the account. ✅
   1. `sudo passwd -l devuser`
3. Check the account status. ✅
   1. `sudo passwd -S devuser`
      1. `devuser L 2026-08-24 0 99999 7 -1`
         1. `L - means its locked`
4. Unlock the account. ✅
   1. `sudo passwd -u devuser`
5. Check the status again. ✅
   1. `sudo passwd -S devuser`
      1. `devuser P 2026-08-24 0 99999 7 -1`
         1. `P - meas account is active and have set password.`

### 

---

## Exercise 11 — Account Information ✅

Use `getent` to inspect users and groups.

### Tasks

Find:

1. `devuser`   ✅
   1. `getent passwd devuser`
2. `developers` ✅
   1. `getent group developers`
3. your own user ✅
   1. `getnet passwd "$(whoami)"`
      1. `Linux will first check who the user is and then check account`
4. the `sudo` group, if it exists ✅
   1. `getent group sudo`

### 

---

## Exercise 12 — Inspect `/etc/passwd` ✅

Use:

```bash
cat /etc/passwd
```

### Tasks

Find your own user and identify: ✅

```text
username
UID
GID
description
home directory
shell
```

```bash
cat etc/passwd | grep "$(whoami)" -> dominik:x:1000:1000:Dominik J:/home/dominik:/bin/bash

username: dominik
password: x
UID: 1000
GID: 1000
Description: Dominik J
home directory: /home/dominik
shell: /bin/bash


```

### Bonus

Find `devuser`: ✅

```bash
grep '^devuser:' /etc/passwd 


devuser:x:1001:1002:Dominik Dev,1,1,1,1:/home/devuser:/bin/bash

```

---

## Exercise 13 — Inspect `/etc/group` ✅

Use:

```bash
cat /etc/group
```

### Tasks

Find:

```text
developers
docker
sudo
```

if they exist on your system.

For each group, identify:

- GID,
- members.



```bash
cat /etc/group | grep developers;  cat /etc/group | grep docker; cat /etc/group | grep sudo

developers:x:1002:devuser

docker:x:972:

sudo:x:27:dominik

```

### Bonus

Query them directly:

```bash
getent group developers
getent group docker
getent group sudo
```

---

## Exercise 14 — `sudo` Permissions ✅

Check what your current user is allowed to do with `sudo`.

### Command

```bash
sudo -l
```

### Tasks

1. Run the command. ✅
   1. `sudo -l`
2. Identify whether your user has administrative privileges. ✅
   1. `User dominik may run the following commands on Zenbook:
          (ALL : ALL) ALL`
3. Find out which commands you are allowed to run with `sudo`. ✅
   1. `(ALL : ALL) ALL`

> Do not modify the sudo configuration for this exercise.

---

## Exercise 15 — Run a Command as Another User ✅

Use `sudo` to run commands as `devuser`.

### Tasks

Run:

```bash
whoami
```

as `devuser`.

```bash
sudo -u devuser whoami
```



Then run:

```bash
id
```

as `devuser`.



```bash
sudo -u devuser id


uid=1001(devuser) gid=1002(developers) groups=1002(developers),100(users),1003(dockerusers)

```

### ### Expected result

The commands should report `devuser`, not your normal username. ✅

---

## Exercise 16 — Switch Users ✅

Switch to `devuser`.

### Tasks

1. Switch to the user. ✅
   1. `sudo - devuser`
2. Confirm who you are. ✅
   1. `whoami`
3. Check your groups.  ✅
   1. `groups "$(whoami)"`
4. Return to your original user. ✅
   1. `sudo - dominik`

### ---

## Exercise 17 — Root Shell

Practice opening and leaving a root shell.

### Tasks

1. Open a root shell.
2. Verify that you are root.
3. Run `id`.
4. Exit the root shell.

### 

---

## Exercise 18 — Logged-in Users

Find out who is currently logged into the system.

### Tasks

Run:

```bash
who
```

Then:

```bash
w
```

Finally:

```bash
users
```

### Question

What is the difference between the information displayed by these commands?

---

## Exercise 19 — Service Accounts

Linux uses accounts that are not intended for normal human login.

### Tasks

Look for service accounts such as:

```text
www-data
postgres
mysql
nginx
```

Use:

```bash
getent passwd
```

or:

```bash
getent passwd | grep -E 'www-data|postgres|mysql|nginx'
```

For any account you find, run:

```bash
id USERNAME
```

and:

```bash
getent passwd USERNAME
```

### Question

Why is it safer for a service to run under a dedicated user instead of `root`?

---

# Mini Project — Linux Team Setup

Now combine everything you have learned.

Imagine you are setting up a small Linux server for a development team.

## Requirements

Create these users:

```text
alice
bob
charlie
```

Create these groups:

```text
developers
dockerusers
backupusers
```

### Group membership

| User      | developers | dockerusers | backupusers |
| --------- | ----------:| -----------:| -----------:|
| `alice`   | ✓          | ✓           | ✗           |
| `bob`     | ✓          | ✗           | ✓           |
| `charlie` | ✓          | ✓           | ✓           |

### Tasks

1. Create all three users.
2. Create all three groups.
3. Add each user to the correct groups.
4. Verify every user's membership with `id`.
5. Verify the groups with `getent group`.
6. Set passwords for all three users.
7. Lock `charlie`.
8. Verify `charlie`'s account status.
9. Unlock `charlie`.
10. Verify the account status again.

### Final verification

For each user, run:

```bash
id alice
id bob
id charlie
```

For each group:

```bash
getent group developers
getent group dockerusers
getent group backupusers
```

---

# Challenge — Least Privilege

Imagine you are running three services:

```text
web application
database
backup service
```

You have these groups:

```text
web
database
backup
```

### Goal

Design the group membership so that each service has access only to what it needs.

### Questions

1. Should every service user belong to every group?
2. Should a web service normally run as `root`?
3. Why should access be granted through groups instead of giving everyone full permissions?
4. What could happen if a compromised service runs as `root`?

Write your answers in your notes.

---

# Cleanup

After finishing the exercises, remove the practice users and groups.

### Remove users

```bash
sudo deluser --remove-home devuser
sudo deluser --remove-home alice
sudo deluser --remove-home bob
sudo deluser --remove-home charlie
```

### Remove groups

```bash
sudo groupdel developers
sudo groupdel dockerusers
sudo groupdel backupusers
```

> Only run the cleanup commands after you have finished the exercises. Make sure these are practice accounts and groups before deleting them.

---

# Final Checklist

Before moving to the next Linux chapter, you should be comfortable with:

- [ ] `whoami`
- [ ] `id`
- [ ] `groups`
- [ ] `getent passwd`
- [ ] `getent group`
- [ ] creating users with `adduser`
- [ ] deleting users with `deluser`
- [ ] creating groups with `groupadd`
- [ ] adding users to groups with `usermod -aG`
- [ ] removing users from groups
- [ ] understanding primary vs supplementary groups
- [ ] changing passwords with `passwd`
- [ ] locking and unlocking accounts
- [ ] using `sudo`
- [ ] checking `sudo` permissions with `sudo -l`
- [ ] switching users with `su`
- [ ] running commands as another user with `sudo -u`
- [ ] identifying service accounts
- [ ] understanding the principle of least privilege

## Most Important Command

If there is one command pattern from this chapter you should remember, it is:

```bash
sudo usermod -aG group username
```

And for inspecting a user:

```bash
id username
```
