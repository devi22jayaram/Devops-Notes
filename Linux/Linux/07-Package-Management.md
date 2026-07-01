# 📦 Package Management in Linux

## What is a Package?

A package is a compressed file that contains everything required to install a software application in Linux.

A package typically includes:

- Executable files
- Libraries
- Configuration files
- Documentation
- Dependencies

Examples of packages:

- Nginx
- Git
- Docker
- Node.js
- MySQL

---

# What is Package Management?

Package Management is the process of:

- Installing software
- Updating software
- Upgrading software
- Removing software
- Managing dependencies

Ubuntu uses **APT (Advanced Package Tool)** as its default package manager.

---

# Why is Package Management Important?

As a Linux Administrator or DevOps Engineer, you should know how to:

- Install software packages
- Update package information
- Upgrade installed packages
- Remove unnecessary software
- Search for available packages
- Troubleshoot package installation issues

---

# Package Repository

A package repository is a server that stores software packages.

When you install a package, Linux downloads it from the configured repository.

```
User

↓

APT

↓

Ubuntu Repository

↓

Downloads Package

↓

Installs Software
```

---

# Update Package List

## apt update

Downloads the latest package information from all configured repositories.

```bash
sudo apt update
```

Example Output:

```
Hit:1 http://archive.ubuntu.com/ubuntu jammy InRelease
Reading package lists... Done
```

---

# Upgrade Installed Packages

## apt upgrade

Updates all installed packages to the latest available versions.

```bash
sudo apt upgrade
```

---

# Install a Package

Example:

```bash
sudo apt install nginx
```

Install Git:

```bash
sudo apt install git
```

Install Tree:

```bash
sudo apt install tree
```

---

# Install Multiple Packages

```bash
sudo apt install nginx git tree
```

---

# Verify Installation

Check Git version:

```bash
git --version
```

Check Nginx version:

```bash
nginx -v
```

Check Tree version:

```bash
tree --version
```

---

# Search for a Package

```bash
apt search docker
```

Example:

```
docker.io
docker-compose
docker-doc
```

---

# View Package Information

```bash
apt show nginx
```

Displays:

- Version
- Description
- Dependencies
- Maintainer

---

# List Installed Packages

```bash
apt list --installed
```

---

# Remove a Package

```bash
sudo apt remove tree
```

Configuration files remain on the system.

---

# Purge a Package

```bash
sudo apt purge tree
```

Removes:

- Software
- Configuration files

---

# Remove Unused Dependencies

```bash
sudo apt autoremove
```

Removes packages that are no longer required.

---

# Install Local .deb Package

```bash
sudo dpkg -i package.deb
```

If dependencies are missing:

```bash
sudo apt --fix-broken install
```

---

# Difference Between apt and dpkg

| apt | dpkg |
|------|------|
| Downloads packages from repositories | Installs local .deb files |
| Automatically installs dependencies | Does not install dependencies |
| Recommended for daily use | Mainly used for manual package installation |

---

# Production Example

Suppose you need to deploy a website.

Step 1

Update repositories.

```bash
sudo apt update
```

Step 2

Install Nginx.

```bash
sudo apt install nginx
```

Step 3

Verify installation.

```bash
systemctl status nginx
```

Step 4

Open your browser.

```
http://localhost
```

If you see the Nginx Welcome Page, the installation is successful.

---

# Common Errors

## Unable to locate package

Example:

```
E: Unable to locate package nginx
```

Solution:

```bash
sudo apt update
```

---

## Could not get lock

Example:

```
Could not get lock /var/lib/dpkg/lock
```

Reason:

Another package installation is running.

Wait until it completes.

---

## dpkg Interrupted

Example:

```
dpkg was interrupted
```

Solution:

```bash
sudo dpkg --configure -a
```

---

## Broken Dependencies

Solution:

```bash
sudo apt --fix-broken install
```

---

# Practical Lab

## Task 1

Update the package list.

```bash
sudo apt update
```

---

## Task 2

Install Tree.

```bash
sudo apt install tree
```

Verify installation.

```bash
tree --version
```

---

## Task 3

Install Git.

```bash
sudo apt install git
```

Verify.

```bash
git --version
```

---

## Task 4

Install Nginx.

```bash
sudo apt install nginx
```

Verify.

```bash
nginx -v
```

---

## Task 5

Search for Docker.

```bash
apt search docker
```

---

## Task 6

Display package information.

```bash
apt show nginx
```

---

## Task 7

Remove Tree.

```bash
sudo apt remove tree
```

---

## Task 8

Run autoremove.

```bash
sudo apt autoremove
```

---

# Interview Questions

1. What is a package?

2. What is Package Management?

3. What is APT?

4. Difference between apt update and apt upgrade?

5. Difference between remove and purge?

6. What is autoremove?

7. What is dpkg?

8. How do you install a local .deb package?

9. How do you search for a package?

10. How do you display package information?

---

# Practice Challenge

Without referring to the notes:

- Update package repositories.
- Install Nginx.
- Verify installation.
- Install Git.
- Search for Docker.
- Remove Tree.
- Run autoremove.
- Explain the difference between apt and dpkg.

---

# Summary

In this chapter you learned:

- Package Management
- APT
- Package Repository
- apt update
- apt upgrade
- apt install
- apt remove
- apt purge
- apt autoremove
- apt search
- apt show
- dpkg
- Production Usage
- Common Errors
- Troubleshooting
