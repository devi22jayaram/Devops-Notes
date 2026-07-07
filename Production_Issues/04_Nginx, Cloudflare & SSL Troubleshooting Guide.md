# Production Incident Resolution: React Static Website, Nginx, Cloudflare & Let's Encrypt SSL

## Overview

During the deployment of a React (Vite) static website to a production server, the domain unexpectedly displayed a backend API response instead of the frontend application. This document outlines the troubleshooting process, root cause, resolution, and lessons learned for future reference.

---

# Problem Statement

### Expected Behavior

- The domain should load the React static website.

### Actual Behavior

- Accessing the domain over HTTPS displayed a backend JSON response instead of the frontend application.

Example:

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

# Troubleshooting Process

## 1. Verify Frontend Build

Confirmed that the application was successfully built.

```bash
npm run build
```

Verified that the build output (`dist/`) contained:

- index.html
- assets/
- static resources

---

## 2. Verify Nginx Configuration

Checked the active Nginx configuration.

```bash
sudo nginx -T
```

Verified:

- server_name
- root directory
- index file
- location block
- try_files configuration

Example:

```nginx
server {
    listen 80;
    server_name example.com www.example.com;

    root /path/to/project/dist;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

---

## 3. Test HTTP

Checked whether HTTP was serving the frontend.

```bash
curl -I http://example.com
```

Response:

```
HTTP/1.1 200 OK
Content-Type: text/html
```

HTTP was working correctly.

---

## 4. Test HTTPS

Checked HTTPS.

```bash
curl https://example.com
```

Instead of the frontend HTML, the response returned backend JSON.

This confirmed that HTTPS traffic was not reaching the intended frontend configuration.

---

## 5. Verify Existing SSL Certificates

Checked installed Let's Encrypt certificates.

```bash
sudo certbot certificates
```

Observation:

- No SSL certificate existed for the domain.

---

## 6. Generate SSL Certificate

Attempted:

```bash
sudo certbot --nginx \
-d example.com \
-d www.example.com
```

Initial result:

```
403 Forbidden
```

Let's Encrypt could not validate the HTTP challenge.

---

## 7. Investigate Cloudflare

Verified:

- DNS records
- Proxy status
- SSL mode

Findings:

- DNS records were proxied through Cloudflare.
- SSL mode was configured as Full.

To allow Let's Encrypt validation:

- Changed DNS records temporarily from **Proxied** to **DNS Only**.

---

## 8. Retry SSL Generation

Executed:

```bash
sudo certbot --nginx \
-d example.com \
-d www.example.com
```

Result:

```
Successfully received certificate
Successfully deployed certificate
Congratulations! HTTPS has been enabled.
```

---

## 9. Verify HTTPS

Verified using:

```bash
curl -I https://example.com
```

Response:

```
HTTP/2 200
Content-Type: text/html
```

Website loaded successfully over HTTPS.

---

## 10. Re-enable Cloudflare Proxy

After successful certificate installation:

- Changed DNS records back to **Proxied**
- Updated Cloudflare SSL Mode to:

```
Full (Strict)
```

This ensures encrypted communication between Cloudflare and the origin server while validating the origin certificate.

---

# Root Cause

The production domain did not have a valid SSL certificate installed on the origin server.

As a result:

- HTTPS requests were not served correctly.
- Cloudflare could not establish a trusted SSL connection to the origin.
- Let's Encrypt validation initially failed because the HTTP challenge was blocked while the domain was proxied through Cloudflare.

---

# Resolution

- Verified frontend build.
- Verified Nginx virtual host configuration.
- Confirmed document root.
- Tested HTTP and HTTPS independently.
- Checked DNS configuration.
- Investigated Cloudflare proxy and SSL mode.
- Temporarily disabled Cloudflare proxy.
- Generated SSL certificate using Certbot.
- Installed the certificate automatically in Nginx.
- Re-enabled Cloudflare proxy.
- Updated Cloudflare SSL mode to **Full (Strict)**.
- Verified successful HTTPS deployment.

---

# Verification Commands

### Check Nginx configuration

```bash
sudo nginx -t
```

---

### Reload Nginx

```bash
sudo systemctl reload nginx
```

---

### View active Nginx configuration

```bash
sudo nginx -T
```

---

### Check installed certificates

```bash
sudo certbot certificates
```

---

### Generate SSL certificate

```bash
sudo certbot --nginx \
-d example.com \
-d www.example.com
```

---

### Verify HTTPS

```bash
curl -I https://example.com
```

---

### Test SSL renewal

```bash
sudo certbot renew --dry-run
```

---

# Lessons Learned

- Always verify that the frontend build has been generated before deployment.
- Ensure the Nginx document root points to the correct build directory (`dist` for Vite).
- Test both HTTP and HTTPS independently during troubleshooting.
- Confirm that DNS records point to the correct origin server.
- If using Cloudflare with Let's Encrypt:
  - Temporarily switch DNS records to **DNS Only** if HTTP challenge validation fails.
  - After successful certificate generation, switch DNS back to **Proxied**.
  - Use **Full (Strict)** SSL mode whenever a valid origin certificate is installed.
- Verify HTTPS functionality before announcing production deployment.
- Test automatic SSL renewal after certificate installation.

---

# Key Takeaways

This incident highlighted the importance of understanding how different infrastructure components work together.

A successful production deployment requires knowledge of:

- DNS
- Cloudflare
- Nginx Virtual Hosts
- SSL/TLS
- Let's Encrypt
- HTTP vs HTTPS routing
- Static website deployment

A structured troubleshooting approach—verifying one layer at a time—helps identify the root cause efficiently and minimizes downtime.

---

# Final Status

- ✅ React application deployed successfully
- ✅ HTTPS enabled
- ✅ SSL certificate installed
- ✅ Cloudflare Proxy enabled
- ✅ Cloudflare SSL Mode: Full (Strict)
- ✅ Automatic SSL renewal configured
- ✅ Production issue resolved successfully
