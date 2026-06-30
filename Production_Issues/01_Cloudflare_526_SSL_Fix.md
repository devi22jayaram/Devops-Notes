# 🔧 Production Issue: Cloudflare Error 526 (Invalid SSL Certificate)

## Overview

While updating a production application, I encountered a **Cloudflare Error 526 (Invalid SSL Certificate)** after pointing a backend subdomain to an active domain.

---

# Problem Statement

The backend URL was configured under a subdomain of an expired domain. To restore the service, I updated the DNS configuration in Cloudflare by pointing the subdomain to an active domain using an **A record**.

After updating the DNS and reloading Nginx, the website returned:

```
Cloudflare Error 526
Invalid SSL Certificate
```

---

# Investigation

### 1. Verified Nginx Configuration

```bash
sudo nginx -t
```

Configuration was valid.

---

### 2. Restarted Nginx

```bash
sudo systemctl restart nginx
```

The issue persisted.

---

### 3. Checked Existing SSL Certificates

```bash
sudo certbot certificates
```

Result:

- ✅ SSL certificate existed for the main domain.
- ❌ No SSL certificate for the new subdomain.

---

### 4. Verified Cloudflare SSL Mode

Cloudflare SSL/TLS mode:

```
Full (Strict)
```

Since Full (Strict) requires a valid SSL certificate on the origin server, Cloudflare rejected the connection.

---

# Root Cause

The newly configured subdomain did not have a valid SSL certificate installed on the origin server.

Cloudflare could not establish a trusted HTTPS connection, resulting in **Error 526**.

---

# Solution

Generated a new Let's Encrypt SSL certificate for the subdomain.

Example:

```bash
sudo certbot --nginx -d subdomain.example.com
```

Verified the configuration:

```bash
sudo nginx -t
```

Reloaded Nginx:

```bash
sudo systemctl restart nginx
```

---

# Result

- ✅ SSL certificate installed successfully
- ✅ Nginx configuration validated
- ✅ Backend service became accessible
- ✅ Cloudflare Error 526 resolved

---

# Lessons Learned

- Always verify SSL coverage when creating or changing subdomains.
- Cloudflare **Full (Strict)** requires a valid SSL certificate on the origin server.
- After DNS changes, verify:
  - DNS records
  - Nginx configuration
  - SSL certificates
  - Cloudflare SSL mode

---

# Commands Used

```bash
sudo nginx -t

sudo systemctl restart nginx

sudo certbot certificates

sudo certbot --nginx -d subdomain.example.com
```

---

# Technologies Used

- Linux (Ubuntu)
- Nginx
- Cloudflare
- Let's Encrypt
- Certbot
- DNS Management

---

# Skills Demonstrated

- Production troubleshooting
- DNS management
- SSL certificate management
- Nginx administration
- Cloudflare configuration
