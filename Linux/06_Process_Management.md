# ⚙️ Process Management in Linux

## What is a Process?

A process is a running instance of a program.

Examples:
- Nginx
- Node.js
- MySQL
- PM2
- SSH

Every running application in Linux is a process.

---

# Why is Process Management Important?

As a Linux Administrator or DevOps Engineer, you should be able to:

- View running processes
- Monitor CPU and Memory usage
- Stop unnecessary processes
- Restart applications
- Troubleshoot high CPU or Memory usage

---

# View Running Processes

## 1. ps Command

Displays currently running processes.

```bash
ps
```

---

## View All Processes

```bash
ps -ef
```

Example:

```
UID        PID   PPID  CMD
root         1      0  systemd
root       854      1  nginx
ubuntu    1520      1  node
```

Explanation:

- PID → Process ID
- PPID → Parent Process ID
- CMD → Command

---

## Search for a Specific Process

```bash
ps -ef | grep nginx
```

```bash
ps -ef | grep node
```

---

# Monitor Processes

## top

```bash
top
```

Shows:

- CPU Usage
- Memory Usage
- Running Processes
- Load Average

Press:

```
q
```

to exit.

---

## htop

A more user-friendly version of `top`.

Install:

```bash
sudo apt update

sudo apt install htop
```

Run:

```bash
htop
```

Useful keys:

```
F3 → Search

F5 → Tree View

F6 → Sort

F9 → Kill Process

F10 → Exit
```

---

# Kill a Process

Find the PID.

```bash
ps -ef | grep nginx
```

Example:

```
PID = 1520
```

Kill it.

```bash
kill 1520
```

---

## Force Kill

```bash
kill -9 1520
```

Use only when the normal kill command does not work.

---

## Kill by Process Name

```bash
pkill nginx
```

or

```bash
killall nginx
```

---

# Run Process in Background

```bash
sleep 100 &
```

Check:

```bash
jobs
```

---

# Bring Background Job to Foreground

```bash
fg
```

---

# Move Running Job to Background

Press

```
Ctrl + Z
```

Then

```bash
bg
```

---

# Run Command Even After Logout

```bash
nohup node app.js &
```

Output:

```
nohup.out
```

This keeps the application running after closing the terminal.

---

# View Process Tree

```bash
pstree
```

Install:

```bash
sudo apt install psmisc
```

---

# Check Process by PID

```bash
ps -p 1520
```

---

# Production Example

Suppose a website becomes slow.

Step 1

Check CPU and Memory.

```bash
htop
```

Step 2

Find the application.

```bash
ps -ef | grep node
```

Step 3

If a process is consuming excessive CPU or memory, identify the cause.

If necessary:

```bash
kill PID
```

or restart the application using PM2:

```bash
pm2 restart app-name
```

This is a common troubleshooting workflow in production environments.

---

# Practical Lab

Create a background process.

```bash
sleep 300 &
```

View jobs.

```bash
jobs
```

Find the process.

```bash
ps -ef | grep sleep
```

Terminate the process.

```bash
kill PID
```

Verify.

```bash
ps -ef | grep sleep
```

---

# Interview Questions

1. What is a process?

2. What is PID?

3. Difference between program and process?

4. Difference between top and htop?

5. What does `kill -9` do?

6. Difference between `kill`, `killall`, and `pkill`?

7. How do you find a running process?

8. How do you run a process in the background?

9. What is `nohup`?

10. Which command shows all running processes?

---

# Practice Task

## Objective

Practice monitoring and managing Linux processes.

### Task 1

Display all running processes.

```bash
ps -ef
```

---

### Task 2

Search for the SSH process.

```bash
ps -ef | grep ssh
```

---

### Task 3

Open htop.

```bash
htop
```

Observe CPU and Memory usage.

---

### Task 4

Run a background process.

```bash
sleep 500 &
```

Verify.

```bash
jobs
```

---

### Task 5

Find the process.

```bash
ps -ef | grep sleep
```

---

### Task 6

Terminate the process.

```bash
kill PID
```

---

### Challenge

Without referring to the notes:

- Run a process in the background.
- Find its PID.
- Check CPU and Memory usage.
- Kill the process.
- Verify that it has stopped.

---

# Summary

In this chapter you learned:

- Process Management
- ps
- top
- htop
- kill
- killall
- pkill
- jobs
- bg
- fg
- nohup
- Process Monitoring
- Production Troubleshooting
