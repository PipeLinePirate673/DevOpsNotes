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
