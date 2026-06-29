# 🔍 Find and Grep in Linux

## What is the find command?

The `find` command is used to search for files and directories in Linux.

### Syntax

```bash
find [path] [options] [expression]
```

---

## Find a file by name

```bash
find /home -name file.txt
```

---

## Find all .log files

```bash
find /var/log -name "*.log"
```

---

## Find directories only

```bash
find . -type d
```

---

## Find files only

```bash
find . -type f
```

---

## Find files larger than 100 MB

```bash
find / -size +100M
```

---

## Find files modified in the last 7 days

```bash
find . -mtime -7
```

---

# What is grep?

`grep` searches for specific text inside files.

### Syntax

```bash
grep "text" filename
```

---

## Search for a word

```bash
grep "error" app.log
```

---

## Ignore uppercase/lowercase

```bash
grep -i "error" app.log
```

---

## Show line numbers

```bash
grep -n "error" app.log
```

---

## Search recursively

```bash
grep -r "database" .
```

---

## Count matching lines

```bash
grep -c "error" app.log
```

---

# Practical Lab

Create a file.

```bash
touch notes.txt
```

Add content.

```text
Linux
Git
Docker
Linux Commands
```

Search for Linux.

```bash
grep Linux notes.txt
```

Find the file.

```bash
find . -name notes.txt
```

---

# Production Example

Suppose your Node.js application is failing.

Find log files:

```bash
find /var/log -name "*.log"
```

Search for errors:

```bash
grep -i error /var/log/nginx/error.log
```

This is one of the most common troubleshooting steps in Linux administration.

---

# Interview Questions

1. What is the difference between `find` and `grep`?
2. How do you search for a file?
3. How do you search for text inside a file?
4. Which command searches recursively?
5. How do you find files larger than 100 MB?

---

# Summary

In this chapter you learned:

- find command
- grep command
- Common options
- Practical examples
- Production troubleshooting
