# 📦 Package Management in Linux

## What is Package Management?

Package Management is the process of installing, updating, upgrading, and removing software packages in a Linux system.

Ubuntu uses **APT (Advanced Package Tool)** as its default package manager.

Examples of software packages:

- Nginx
- Git
- Docker
- Node.js
- MySQL
- Tree

---

# Why is Package Management Important?

As a Linux Administrator or DevOps Engineer, you should be able to:

- Install new software
- Update package information
- Upgrade installed packages
- Remove unused software
- Search available packages
- Troubleshoot package installation issues

---

# What is a Package?

A package is a compressed file that contains everything required to install a software application.

A package contains:

- Executable files
- Libraries
- Configuration files
- Documentation
- Dependencies

---

# What is APT?

APT (Advanced Package Tool) is the package manager used in Ubuntu and Debian-based Linux distributions.

It helps you:

- Install packages
- Remove packages
- Update packages
- Upgrade packages
- Manage dependencies

---

# Update Package Repository

## apt update

Downloads the latest package information from configured repositories.

```bash
sudo apt update
```

Example Output

```
Hit:1 http://archive.ubuntu.com/ubuntu jammy InRelease
Reading package lists... Done
```

---

# Upgrade Installed Packages

## apt upgrade

Updates installed packages to the latest available version.

```bash
sudo apt upgrade
```

---

# Install a Package

Install Nginx

```bash
sudo apt install nginx
```

Install Git

```bash
sudo apt install git
```

Install Tree

```bash
sudo apt install tree
```

---

# Install Multiple Packages

```bash
sudo apt install nginx git tree
```

---

# Verify Installed Package

Check Git Version

```bash
git --version
```

Check Nginx Version

```bash
nginx -v
```

Check Tree Version

```bash
tree --version
```

---

# Search for a Package

```bash
apt search docker
```

Example Output

```
docker.io
docker-compose
docker-doc
```

---

# View Package Details

```bash
apt show nginx
```

Displays

- Package Version
- Description
- Maintainer
- Dependencies

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

Removes the software but keeps configuration files.

---

# Purge a Package

```bash
sudo apt purge tree
```

Removes:

- Package
- Configuration files

---

# Remove Unused Packages

```bash
sudo apt autoremove
```

Removes unused dependencies.

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
|-----|------|
| Downloads packages from repositories | Installs local .deb packages |
| Automatically installs dependencies | Does not install dependencies |
| Recommended for daily use | Used for manual package installation |

---

# Production Example

Suppose a new Ubuntu server is provisioned.

The first step is to update the package repository.

```bash
sudo apt update
```

Install Nginx.

```bash
sudo apt install nginx
```

Verify the installation.

```bash
systemctl status nginx
```

Check the installed version.

```bash
nginx -v
```

Open the browser.

```
http://localhost
```

If the Nginx Welcome page appears, the installation is successful.

---

# Common Errors

## Unable to Locate Package

```
E: Unable to locate package
```

Solution

```bash
sudo apt update
```

---

## Could not get lock

```
Could not get lock /var/lib/dpkg/lock
```

Reason

Another package installation is running.

Wait until it completes.

---

## dpkg was interrupted

Solution

```bash
sudo dpkg --configure -a
```

---

## Broken Dependencies

Solution

```bash
sudo apt --fix-broken install
```

---

# Practical Lab

## Task 1

Update package information.

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

View Nginx Package Information.

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

Remove unused dependencies.

```bash
sudo apt autoremove
```

---

# Interview Questions

1. What is Package Management?

2. What is APT?

3. What is a package?

4. Difference between apt update and apt upgrade?

5. Difference between apt remove and apt purge?

6. What is apt autoremove?

7. What is dpkg?

8. How do you install a local .deb package?

9. How do you search for a package?

10. How do you view package information?

---

# Practice Challenge

Without referring to the notes:

- Update the package repository.
- Install Git.
- Install Tree.
- Install Nginx.
- Verify all installed packages.
- Search for Docker.
- Remove Tree.
- Run apt autoremove.

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
- Common Errors
- Troubleshooting
- Production Example
