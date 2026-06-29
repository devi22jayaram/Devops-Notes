# 🔐 File Permissions in Linux

## What are File Permissions?

Linux uses file permissions to control who can:

- Read a file
- Write to a file
- Execute a file

This helps keep the system secure.

---

# Permission Types

| Permission | Symbol | Value |
|------------|--------|-------|
| Read | r | 4 |
| Write | w | 2 |
| Execute | x | 1 |

---

# Permission Categories

Every file has permissions for:

- Owner (u)
- Group (g)
- Others (o)

Example:

-rwxr-xr--

Breakdown:

Owner : rwx

Group : r-x

Others : r--

---

# View Permissions

```bash
ls -l
```

Example Output

```bash
-rwxr-xr-- 1 devi frontend 245 Jun 30 test.sh
```

---

# chmod Command

Used to change permissions.

Syntax

```bash
chmod permission filename
```

Example

```bash
chmod 755 test.sh
```

---

# Numeric Permissions

| Number | Permission |
|----------|-----------|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 3 | -wx |
| 2 | -w- |
| 1 | --x |
| 0 | --- |

Examples

```bash
chmod 777 file.txt

chmod 755 script.sh

chmod 644 notes.txt

chmod 600 secret.txt
```

---

# Symbolic Method

Give execute permission

```bash
chmod +x script.sh
```

Remove write permission

```bash
chmod -w file.txt
```

Add write permission

```bash
chmod u+w file.txt
```

---

# chown Command

Change file owner.

Syntax

```bash
sudo chown username file.txt
```

Example

```bash
sudo chown student1 project.txt
```

---

# Change Owner and Group

```bash
sudo chown student1:frontend project.txt
```

---

# chgrp Command

Change group ownership.

```bash
sudo chgrp backend project.txt
```

---

# Practical Exercise

Create directory

```bash
mkdir project
```

Create file

```bash
touch project/app.js
```

View permissions

```bash
ls -l project
```

Give execute permission

```bash
chmod +x project/app.js
```

Change owner

```bash
sudo chown student1 project/app.js
```

Change group

```bash
sudo chgrp frontend project/app.js
```

---

# Real-World Example

Suppose your company has two teams.

Frontend Team

Backend Team

Create two folders.

```bash
mkdir frontend backend
```

Assign ownership.

```bash
sudo chown :frontend frontend

sudo chown :backend backend
```

Allow only the respective teams to access their folders.

This is how permissions are commonly managed in production environments.

---

# Interview Questions

1. What is chmod?

2. What is chown?

3. What is chgrp?

4. Difference between 755 and 777?

5. What do rwxr-xr-x mean?

6. Which command changes ownership?

7. What is the difference between symbolic and numeric permissions?

---

# Summary

In this chapter you learned:

- Linux permissions
- chmod
- chown
- chgrp
- Numeric permissions
- Symbolic permissions
- Practical permission management
