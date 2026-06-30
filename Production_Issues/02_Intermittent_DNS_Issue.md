# 🌐 Production Issue: Intermittent DNS Resolution

## Overview

A production website was experiencing intermittent availability.

Observed behavior:

- ✅ Sometimes the website loaded successfully.
- ❌ Sometimes Cloudflare displayed a DNS error.

Since the issue was inconsistent, a structured troubleshooting approach was required to identify the root cause.

---

# Environment

- Linux
- Nginx
- Cloudflare
- DNS
- HTTPS

---

# Problem

Users reported that the website was not consistently accessible.

The issue was intermittent, making it difficult to reproduce immediately.

---

# Troubleshooting Process

## Step 1: Verify DNS Resolution

Checked DNS records using:

```bash
dig example.com
```

Verified that the domain resolved to the expected IP address.

---

## Step 2: Review Cloudflare DNS

Verified:

- A Records
- Proxy Status
- DNS configuration

---

## Step 3: Verify Server Response

Tested the application directly from the server.

```bash
curl -I https://example.com
```

Confirmed whether the origin server responded correctly.

---

## Step 4: Validate Nginx Configuration

Checked Nginx configuration.

```bash
sudo nginx -t
```

Verified virtual host configuration.

---

## Step 5: Verify Backend Services

Confirmed that backend services were running correctly.

Example:

```bash
pm2 status
```

or

```bash
systemctl status <service>
```

---

## Step 6: Compare DNS and Server Configuration

Compared:

- Cloudflare DNS records
- Server IP
- Nginx configuration
- SSL configuration

---

## Step 7: Identify the Root Cause

Found unnecessary DNS records that conflicted with the active configuration.

These conflicting records caused inconsistent DNS resolution.

---

## Step 8: Resolution

- Removed unnecessary DNS records.
- Verified Cloudflare configuration.
- Confirmed Nginx configuration.
- Tested multiple times from different locations.

---

# Verification

Performed multiple validation checks.

```bash
dig example.com

curl -I https://example.com

sudo nginx -t
```

The website responded consistently after the changes.

---

# Root Cause

Conflicting DNS records in Cloudflare caused intermittent DNS resolution.

---

# Lessons Learned

- Never assume the first symptom is the root cause.
- Verify DNS before modifying the server.
- Validate every infrastructure layer.
- Test repeatedly after making changes.
- Keep DNS records clean to avoid conflicts.

---

# Technologies Used

- Linux
- Cloudflare
- DNS
- Nginx
- HTTP/HTTPS

---

# Skills Demonstrated

- Production Troubleshooting
- DNS Analysis
- Nginx Administration
- Cloudflare Configuration
- Root Cause Analysis
- Infrastructure Validation

---

# Commands Used

```bash
dig example.com

curl -I https://example.com

sudo nginx -t

sudo systemctl restart nginx
```

---

# Outcome

✅ Website became consistently accessible.

✅ DNS resolution stabilized.

✅ Production service restored successfully.
