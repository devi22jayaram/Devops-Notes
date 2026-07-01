# 📅 Phase 1 - Advanced Linux Administration

# Day 1 - Introduction to System Services

## 🎯 Objective

By the end of this session, you will understand:

- What is a Service?
- Difference between Process and Service
- What is systemd?
- What is systemctl?
- Why Services are important in Linux?
- Real-world examples of Linux services

---

# What is a Service?

A **Service** is a program that runs in the background and performs specific tasks without requiring user interaction.

Unlike normal applications, services usually start automatically when the operating system boots and continue running until they are stopped or the system is shut down.

Examples of Linux services:

- Nginx
- Apache
- SSH
- Docker
- MySQL
- Cron

---

# Real-Life Example

Imagine you open your browser and visit:

```
https://example.com
```

How does the website open?

```
User

↓

Internet

↓

Linux Server

↓

Nginx Service

↓

Node.js Service

↓

Database Service

↓

Website Response
```

Behind every website, several Linux services work together continuously.

---

# What is a Process?

A **Process** is a running instance of a program.

Example:

When you execute

```bash
node app.js
```

Linux creates a new process.

Every running application has:

- Process ID (PID)
- Memory
- CPU Usage
- Parent Process

---

# Difference Between Process and Service

| Process | Service |
|----------|----------|
| Running instance of a program | Background program that provides a service |
| Can be started manually | Usually starts automatically during boot |
| May stop after completing its task | Usually runs continuously |
| Example: nano, vim | Example: nginx, ssh, mysql |

---

# Why are Services Important?

Without services:

- Websites will not load.
- SSH remote access will not work.
- Databases will stop responding.
- Scheduled tasks will not run.

Linux servers rely on services to provide applications and system functionality.

---

# What is systemd?

**systemd** is the default system and service manager in modern Linux distributions.

It is responsible for:

- Starting services during boot
- Stopping services
- Restarting services
- Monitoring services
- Managing dependencies
- Logging service events

---

# Why is systemd Important?

systemd helps Linux:

- Boot faster
- Automatically start required services
- Restart failed services
- Manage background processes
- Collect logs

---

# Verify systemd

Check the first process started by Linux.

```bash
ps -p 1
```

Example Output

```
PID TTY      TIME CMD
1   ?        00:00:05 systemd
```

Notice that **systemd** always has **PID 1** because it is the first user-space process started after the Linux kernel boots.

---

# What is systemctl?

`systemctl` is the command-line utility used to communicate with systemd.

Using `systemctl`, administrators can:

- Start services
- Stop services
- Restart services
- Enable services
- Disable services
- Check service status
- View service information

---

# Production Example

Suppose users report:

> "The company website is not opening."

The first thing a Linux Administrator checks is whether the web server service is running.

Example:

```bash
systemctl status nginx
```

If the service has stopped unexpectedly, the administrator investigates the logs, fixes the issue, and starts the service again.

---

# Common Linux Services

| Service | Purpose |
|----------|---------|
| nginx | Web Server |
| apache2 | Web Server |
| ssh | Secure Remote Login |
| docker | Container Engine |
| mysql | Database Server |
| cron | Job Scheduler |
| networking | Network Management |

---

# Why Should a DevOps Engineer Learn Services?

Almost every production server depends on services.

Examples:

- Deploying applications
- Managing web servers
- Monitoring databases
- Configuring SSH
- Running Docker
- Scheduling backups

Understanding Linux services is one of the core skills of a Linux Administrator and DevOps Engineer.

---

# Today's Practical Tasks

## Task 1

Check the first process started by Linux.

```bash
ps -p 1
```

Observe the output.

---

## Task 2

Check your Linux version.

```bash
hostnamectl
```

---

## Task 3

Display your current user.

```bash
whoami
```

---

## Task 4

List all running processes.

```bash
ps -ef
```

Observe how many processes are running.

---

## Task 5

Find the SSH process.

```bash
ps -ef | grep ssh
```

---

# Self-Assessment

Answer these questions without referring to the notes:

1. What is a Service?
2. What is a Process?
3. What is the difference between a Process and a Service?
4. What is systemd?
5. Why is systemd important?
6. What is systemctl?
7. Which process always has PID 1?
8. Name five Linux services.

---

# Key Takeaways

Today you learned:

- What is a Service
- What is a Process
- Difference between Process and Service
- What is systemd
- What is systemctl
- Why Linux services are important
- Common Linux services
- The role of services in production environments

---

# Tomorrow's Topic

**Day 2 - Managing Linux Services Using systemctl**

Topics:

- Check service status
- Start a service
- Stop a service
- Restart a service
- Reload a service
- Enable services during boot
- Disable services
- View service information
