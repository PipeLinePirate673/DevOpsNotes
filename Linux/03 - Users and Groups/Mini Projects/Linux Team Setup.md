

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
| --------- | ---------- | ----------- | ----------- |
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
