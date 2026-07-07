# Production Issue - React Static Website Showing Backend JSON Instead of Frontend

**Date:** 07-07-2026

## Issue

The React static website was not loading.

Instead of the frontend, accessing:

```
https://frginfraassociates.com
```

displayed:

```json
{
  "success": true,
  "message": "Server is working fine"
}
```

---

# Environment

- Ubuntu Server
- Nginx
- React (Vite)
- Cloudflare
- Let's Encrypt (Certbot)

---

# Initial Investigation

### 1. Verify Nginx configuration

Checked the active configuration:

```bash
sudo nginx -T
```

Verified:

- server_name
- root directory
- index file
- try_files configuration

Current configuration:

```nginx
server {
    listen 80;
    server_name frginfraassociates.com www.frginfraassociates.com;

    root /home/administrator/Live-Project/Live_Front/demosite/FRG-INFRA-ASSOCIATES/dist;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

---

### 2. Verify React build

Checked build folder.

```bash
ls
```

Verified:

```
dist/
index.html
assets/
```

---

### 3. Verify HTTP

```bash
curl -I http://frginfraassociates.com
```

Response:

```
200 OK
Content-Type: text/html
```

HTTP was working correctly.

---

### 4. Verify HTTPS

```bash
curl https://frginfraassociates.com
```

Instead of HTML, backend JSON was returned.

This indicated HTTPS traffic was not serving the frontend.

---

### 5. Check existing SSL certificates

```bash
sudo certbot certificates
```

Observation:

No certificate existed for:

```
frginfraassociates.com
```

---

### 6. Attempt SSL generation

Executed:

```bash
sudo certbot --nginx \
-d frginfraassociates.com \
-d www.frginfraassociates.com
```

Received:

```
403 Forbidden
```

for

```
.well-known/acme-challenge
```

---

### 7. Investigate Cloudflare

Verified:

- DNS Records
- SSL Mode

Cloudflare was configured as:

```
SSL Mode : Full
Proxy : Enabled
```

---

### 8. Temporary Fix

Changed DNS records from

```
Proxied
```

to

```
DNS Only
```

This allowed Let's Encrypt validation requests to reach the origin server directly.

---

### 9. Retry SSL Generation

Executed:

```bash
sudo certbot --nginx \
-d frginfraassociates.com \
-d www.frginfraassociates.com
```

Certificate was generated successfully.

Output:

```
Successfully received certificate

Successfully deployed certificate

Congratulations!
```

---

### 10. Re-enable Cloudflare

Changed DNS back to

```
Proxied
```

Updated Cloudflare SSL Mode to

```
Full (Strict)
```

---

# Verification

Verified using:

```bash
curl -I https://frginfraassociates.com
```

Response:

```
HTTP/2 200

Server: cloudflare

Content-Type: text/html
```

Website loaded successfully.

---

# Root Cause

The domain did not have a valid SSL certificate installed.

HTTPS traffic was therefore not serving the intended frontend.

Let's Encrypt validation also failed initially because Cloudflare Proxy prevented successful HTTP challenge validation.

---

# Resolution

- Verified Nginx configuration
- Verified React build
- Verified DNS records
- Disabled Cloudflare Proxy temporarily
- Generated SSL certificate using Certbot
- Installed certificate automatically
- Re-enabled Cloudflare Proxy
- Changed SSL Mode to Full (Strict)
- Verified HTTPS functionality

---

# Useful Commands

Check Nginx

```bash
sudo nginx -t
sudo systemctl reload nginx
```

View active configuration

```bash
sudo nginx -T
```

Check certificates

```bash
sudo certbot certificates
```

Generate certificate

```bash
sudo certbot --nginx \
-d frginfraassociates.com \
-d www.frginfraassociates.com
```

Test renewal

```bash
sudo certbot renew --dry-run
```

Check HTTP

```bash
curl -I http://frginfraassociates.com
```

Check HTTPS

```bash
curl -I https://frginfraassociates.com
```

---

# Lessons Learned

- Always build the React application before deployment.
- Nginx root should point to the `dist` folder for Vite projects.
- Verify DNS points to the correct server.
- Generate the SSL certificate before enabling Cloudflare Proxy.
- Use **Cloudflare SSL Mode: Full (Strict)** when using Let's Encrypt.
- Verify HTTPS using `curl` before announcing production deployment.
- Test automatic SSL renewal using `sudo certbot renew --dry-run`.

---

# Final Status

✅ Website is live

✅ HTTPS enabled

✅ Cloudflare Proxy enabled

✅ SSL Mode: Full (Strict)

✅ Automatic certificate renewal configured

✅ Production issue resolved successfully
