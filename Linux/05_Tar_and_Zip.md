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
---

# 🧪 Practice Task

## Objective

Practice creating and extracting archive files using `tar` and `zip`.

### Task 1: Create a Project Directory

```bash
mkdir Project
cd Project
```

### Task 2: Create Three Files

```bash
touch index.html
touch style.css
touch app.js
```

Verify the files:

```bash
ls
```

Expected output:

```
app.js
index.html
style.css
```

### Task 3: Create a TAR Archive

```bash
cd ..
tar -cvf Project.tar Project/
```

Verify:

```bash
ls
```

### Task 4: Create a TAR.GZ Archive

```bash
tar -czvf Project.tar.gz Project/
```

### Task 5: Create a ZIP Archive

```bash
zip -r Project.zip Project/
```

### Task 6: Extract the TAR Archive

```bash
mkdir Tar_Test
tar -xvf Project.tar -C Tar_Test
```

### Task 7: Extract the ZIP Archive

```bash
mkdir Zip_Test
unzip Project.zip -d Zip_Test
```

### Task 8: Verify the Extracted Files

```bash
tree Tar_Test
```

or

```bash
find Tar_Test
```

Expected structure:

```
Project/
├── app.js
├── index.html
└── style.css
```

---

# ✅ Challenge

Without referring to the notes:

- Create a folder named `Website`
- Add four files inside it
- Compress it using both `tar.gz` and `zip`
- Extract both archives
- Verify the contents

If you can complete this without errors, you've mastered the basics of `tar` and `zip`.
