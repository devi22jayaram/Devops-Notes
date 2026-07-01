# ⚙️ System Services (systemd & systemctl) in Linux

## What is a Service?

A service is a program that runs in the background and performs specific tasks without user interaction.

Examples of services:

- Nginx
- Apache
- SSH
- Docker
- MySQL
- Cron

Services usually start automatically when the system boots.

---

# Why are Services Important?

As a Linux Administrator or DevOps Engineer, you should be able to:

- Start services
- Stop services
- Restart services
- Check service status
- Enable services during system boot
- Disable unnecessary services
- Troubleshoot service failures

---

# What is systemd?

**systemd** is the default system and service manager used in modern Linux distributions.

Responsibilities of systemd:

- Starts system services during boot
- Manages background services
- Tracks service status
- Handles system shutdown and reboot
- Collects service logs

---

# What is systemctl?

**systemctl** is the command-line tool used to manage services controlled by systemd.

Using systemctl you can:

- Start services
- Stop services
- Restart services
- Reload services
- Enable services
- Disable services
- Check service status

---

# Check Service Status

```bash
systemctl status nginx
```

Example Output

```
● nginx.service - A high performance web server
   Loaded: loaded
   Active: active (running)
```

---

# Start a Service

```bash
sudo systemctl start nginx
```

Verify

```bash
systemctl status nginx
```

---

# Stop a Service

```bash
sudo systemctl stop nginx
```

---

# Restart a Service

```bash
sudo systemctl restart nginx
```

Use this after changing configuration files.

---

# Reload a Service

```bash
sudo systemctl reload nginx
```

Reload applies configuration changes without completely restarting the service.

---

# Enable Service at Boot

```bash
sudo systemctl enable nginx
```

The service starts automatically whenever the server boots.

---

# Disable Service at Boot

```bash
sudo systemctl disable nginx
```

The service will not start automatically after reboot.

---

# Check Whether a Service is Enabled

```bash
systemctl is-enabled nginx
```

Example Output

```
enabled
```

or

```
disabled
```

---

# Check Whether a Service is Running

```bash
systemctl is-active nginx
```

Example Output

```
active
```

or

```
inactive
```

---

# List Running Services

```bash
systemctl list-units --type=service
```

---

# List All Services

```bash
systemctl list-unit-files --type=service
```

---

# View Service Logs

```bash
journalctl -u nginx
```

View the latest logs.

---

# View Live Logs

```bash
journalctl -fu nginx
```

Press

```
Ctrl + C
```

to exit.

---

# Reload systemd

If you modify a service file:

```bash
sudo systemctl daemon-reload
```

---

# Reboot the System

```bash
sudo systemctl reboot
```

---

# Shutdown the System

```bash
sudo systemctl poweroff
```

---

# Difference Between Restart and Reload

| Restart | Reload |
|----------|---------|
| Stops and starts the service | Reloads configuration only |
| Small downtime | No downtime (if supported) |
| Used after major changes | Used after configuration changes |

---

# Production Example

Suppose your company website is not opening.

Step 1

Check whether Nginx is running.

```bash
systemctl status nginx
```

If inactive:

```bash
sudo systemctl start nginx
```

If configuration changes were made:

```bash
sudo systemctl restart nginx
```

Verify

```bash
systemctl status nginx
```

Open the website and confirm it is accessible.

---

# Common Errors

## Unit Not Found

Example

```
Unit nginx.service could not be found.
```

Reason

The software is not installed.

Solution

```bash
sudo apt install nginx
```

---

## Failed to Start Service

Check logs.

```bash
journalctl -u nginx
```

---

## Permission Denied

Run the command with sudo.

```bash
sudo systemctl restart nginx
```

---

## Service Failed After Configuration Change

Test configuration.

```bash
sudo nginx -t
```

If successful:

```bash
sudo systemctl restart nginx
```

---

# Practical Lab

## Task 1

Check Nginx status.

```bash
systemctl status nginx
```

---

## Task 2

Stop Nginx.

```bash
sudo systemctl stop nginx
```

Verify.

```bash
systemctl status nginx
```

---

## Task 3

Start Nginx.

```bash
sudo systemctl start nginx
```

---

## Task 4

Restart Nginx.

```bash
sudo systemctl restart nginx
```

---

## Task 5

Enable Nginx during boot.

```bash
sudo systemctl enable nginx
```

---

## Task 6

Check if it is enabled.

```bash
systemctl is-enabled nginx
```

---

## Task 7

View Nginx logs.

```bash
journalctl -u nginx
```

---

## Task 8

List all running services.

```bash
systemctl list-units --type=service
```

---

# Interview Questions

1. What is a service in Linux?

2. What is systemd?

3. What is systemctl?

4. How do you start a service?

5. How do you stop a service?

6. Difference between restart and reload?

7. How do you enable a service during boot?

8. How do you disable a service?

9. How do you check service logs?

10. How do you verify whether a service is running?

---

# Practice Challenge

Without referring to the notes:

- Check the status of the SSH service.
- Start the SSH service if it is stopped.
- Restart the SSH service.
- Enable the SSH service at boot.
- Verify that it is enabled.
- View SSH service logs.
- List all running services.

---

# Summary

In this chapter you learned:

- Services
- systemd
- systemctl
- Start Service
- Stop Service
- Restart Service
- Reload Service
- Enable Service
- Disable Service
- Check Service Status
- Service Logs
- journalctl
- Production Troubleshooting
