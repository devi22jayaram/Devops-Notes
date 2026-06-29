# 📦 Tar and Zip in Linux

## What is tar?

The `tar` command is used to archive multiple files and directories into a single file. It is commonly used for backups and deployments.

---

## Common tar Commands

### Create a tar archive

```bash
tar -cvf project.tar project/
```

### Extract a tar archive

```bash
tar -xvf project.tar
```

### Create a compressed tar.gz archive

```bash
tar -czvf project.tar.gz project/
```

### Extract a tar.gz archive

```bash
tar -xzvf project.tar.gz
```

### View archive contents

```bash
tar -tvf project.tar
```

---

# What is zip?

The `zip` command compresses files and folders into a `.zip` archive.

---

## Create a zip file

```bash
zip project.zip file1.txt file2.txt
```

---

## Zip a directory

```bash
zip -r project.zip project/
```

---

## What is unzip?

The `unzip` command extracts `.zip` files.

```bash
unzip project.zip
```

---

## Install zip and unzip (Ubuntu)

```bash
sudo apt update

sudo apt install zip unzip
```

---

# Practical Lab

Create a directory.

```bash
mkdir DevOps
```

Create files.

```bash
touch DevOps/linux.txt

touch DevOps/git.txt
```

Create a tar archive.

```bash
tar -cvf DevOps.tar DevOps/
```

Extract it.

```bash
tar -xvf DevOps.tar
```

Create a zip archive.

```bash
zip -r DevOps.zip DevOps/
```

Extract it.

```bash
unzip DevOps.zip
```

---

# Real-World Example

Before deploying a website, the application files are often compressed into a `.tar.gz` archive and transferred to the server.

Example:

```bash
tar -czvf release.tar.gz build/
```

On the server:

```bash
tar -xzvf release.tar.gz
```

This is a common deployment practice in Linux environments.

---

# Interview Questions

1. What is the difference between tar and zip?
2. How do you create a tar archive?
3. How do you extract a tar.gz file?
4. Which command compresses a folder into a zip file?
5. How do you install zip and unzip on Ubuntu?

---

# Summary

In this chapter you learned:

- tar
- tar.gz
- zip
- unzip
- Common commands
- Practical examples
- Production use cases
