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

```bash
sudo adduser alice

sudo adduser bob

sudo adduser charlie
```



Create these groups:

```text
developers
dockerusers
backupusers
```

```bash
sudo groupadd developers

sudo groupadd dockerusers

sudo groupadd backupusers

```





### Group membership

| User      | developers | dockerusers | backupusers |
| --------- | ---------- | ----------- | ----------- |
| `alice`   | ✓          | ✓           | ✗           |
| `bob`     | ✓          | ✗           | ✓           |
| `charlie` | ✓          | ✓           | ✓           |

### 

```bash
sudo usermod -aG developers,dockerusers alice

sudo usermod -aG developers,backupusers bob

sudo usermod -aG developers,dockerusers,backupusers charlie
```



### Tasks

1. Create all three users. ✅ 
2. Create all three groups. ✅ 
3. Add each user to the correct groups. ✅
4. Verify every user's membership with `id`.
   1. `id alice`
   2. `id bob`
   3. `id charlie`
5. Verify the groups with `getent group`. ✅
   1. `getent group | grep developers`
      1. `developers:x:1002:alice,bob,charlie`
   2. `getent group | grep dockerusers`
      1. `dockerusers:x:1003:alice,charlie`
   3. `getent group | grep backupusers`
      1. `backupusers:x:1004:bob,charlie`
6. Set passwords for all three users.
   1. 
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
