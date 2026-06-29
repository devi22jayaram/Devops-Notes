# 👥 Users and Groups in Linux

## What are Users?

A user is an account that can log in to a Linux system.

Every user has:
- Username
- User ID (UID)
- Home directory
- Default shell

Example:

student1

student2

student3

---

## Types of Users

### 1. Root User

- Super administrator
- Has complete control over the system
- UID = 0

Example:

root

---

### 2. Normal User

- Created for daily work
- Limited permissions

Example:

devi

student1

---

### 3. System User

- Used by services and applications
- Usually cannot log in

Example:

www-data

mysql

nginx

---

# What are Groups?

A group is a collection of users.

Instead of assigning permissions to individual users,
permissions can be assigned to a group.

Example:

Frontend Team

Backend Team

Developers

---

## Why Groups?

Groups make permission management easier.

Example:

Project

├── frontend

└── backend

Frontend developers can access only the frontend folder.

Backend developers can access only the backend folder.

---

# User Management Commands

## Create a User

```bash
sudo useradd student1
```

or

```bash
sudo adduser student1
```

---

## Set Password

```bash
sudo passwd student1
```

---

## Delete User

```bash
sudo userdel student1
```

Delete user along with the home directory:

```bash
sudo userdel -r student1
```

---

## View Current User

```bash
whoami
```

---

## View Logged-in Users

```bash
who
```

---

## User ID Information

```bash
id
```

Example Output

```
uid=1001(student1)
gid=1001(student1)
groups=1001(student1)
```

---

# Group Management Commands

## Create Group

```bash
sudo groupadd frontend
```

---

## Delete Group

```bash
sudo groupdel frontend
```

---

## Add User to Group

```bash
sudo usermod -aG frontend student1
```

---

## Check User Groups

```bash
groups student1
```

---

# Practical Lab

Create three users.

```bash
sudo adduser student1

sudo adduser student2

sudo adduser student3
```

Create two groups.

```bash
sudo groupadd frontend

sudo groupadd backend
```

Assign users.

```bash
sudo usermod -aG frontend student1

sudo usermod -aG frontend student2

sudo usermod -aG backend student3
```

Verify.

```bash
groups student1

groups student2

groups student3
```

---

# Real-World Example

Suppose a company has two teams.

Frontend Team

- Arun
- Devi

Backend Team

- Karthick
- Ravi

Instead of assigning permissions one by one, create two groups:

frontend

backend

Assign users to the appropriate group and manage folder permissions through the groups.

---

# Interview Questions

### What is the difference between a user and a group?

### What is the root user?

### Which command creates a user?

### How do you add a user to a group?

### Which command shows the current user?

### What is UID?

### Why are groups used in Linux?

---

# Summary

In this chapter you learned:

- Types of users
- Root user
- Normal user
- System user
- Groups
- Creating users
- Creating groups
- Adding users to groups
- Useful Linux user management commands
