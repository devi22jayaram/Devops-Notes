# Dedicated Client Server Setup (End-to-End)

## Goal

Deploy a production-ready application with:

* React/Vite frontend
* Node.js + Express backend
* MongoDB database
* File uploads (30–40 GB)
* HTTPS (SSL)
* Cloudflare CDN & DNS
* Dedicated VPS server
* Daily backups
* PM2 process management

---

# Recommended Architecture

User
|
| HTTPS
|
Cloudflare
|
| HTTPS
|
Frontend: Cloudflare Pages
|
| API Calls
|
Backend: VPS (Nginx + PM2 + Node.js)
|
| Database
|
MongoDB Atlas
|
| File Uploads
|
Cloudflare R2 or /var/www/uploads

---

# Server Recommendation

## Hostinger VPS (Recommended for beginners)

| Resource  | Value            |
| --------- | ---------------- |
| CPU       | 2 vCPU           |
| RAM       | 4 GB             |
| Storage   | 50 GB NVMe SSD   |
| Bandwidth | 4 TB             |
| OS        | Ubuntu 22.04 LTS |
| Cost      | ₹500–700/month   |

### Why 50 GB?

* Ubuntu OS: 8–10 GB
* Logs & backups: 5 GB
* Application code: 2 GB
* File uploads: 30–40 GB
* Free space: 5–10 GB

---

# Purchase Steps

1. Go to https://www.hostinger.in/vps-hosting
2. Select **KVM 2**
3. Choose **Ubuntu 22.04**
4. Choose **Singapore** or **India** data center
5. Complete payment
6. Save:

   * Server IP
   * root username
   * root password

---

# Connect to Server

```bash
ssh root@YOUR_SERVER_IP
```

Example:

```bash
ssh root@103.120.10.20
```

---

# Create a Normal User

```bash
adduser devi
usermod -aG sudo devi
```

Switch user:

```bash
su - devi
```

---

# Update Server

```bash
sudo apt update && sudo apt upgrade -y
```

---

# Install Required Software

## Install Nginx

```bash
sudo apt install nginx -y
```

## Install Node.js (LTS)

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

Verify:

```bash
node -v
npm -v
```

## Install PM2

```bash
sudo npm install -g pm2
```

---

# Project Folder Structure

```bash
mkdir -p ~/apps/client-project/backend
mkdir -p ~/apps/client-project/frontend
```

---

# Upload Backend Code

Use **WinSCP** or **VS Code Remote SSH**.

---

# Backend Setup

```bash
cd ~/apps/client-project/backend
npm install
```

Create `.env`:

```bash
nano .env
```

Add:

```env
PORT=4444
MONGO_DB=mongodb+srv://username:password@cluster.mongodb.net/clientdb
JWT_KEY=your-secret-key
NODE_ENV=production
```

Build:

```bash
npm run build
```

Start with PM2:

```bash
pm2 start dist/index.js --name client-api
pm2 save
pm2 startup
```

Check status:

```bash
pm2 status
```

Restart:

```bash
pm2 restart client-api
```

View logs:

```bash
pm2 logs client-api
```

---

# Frontend Deployment

## Build locally

```bash
npm install
npm run build
```

## Deploy to Cloudflare Pages

Upload the `dist/` folder.

### Build settings

| Setting          | Value         |
| ---------------- | ------------- |
| Build command    | npm run build |
| Output directory | dist          |

---

# Nginx Configuration

Create config:

```bash
sudo nano /etc/nginx/sites-available/client-api
```

Paste:

```nginx
server {
    listen 80;
    server_name api.clientdomain.com;

    location / {
        proxy_pass http://127.0.0.1:4444;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

Enable:

```bash
sudo ln -s /etc/nginx/sites-available/client-api /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

Check status:

```bash
sudo systemctl status nginx
```

---

# Cloudflare DNS Setup

## Backend

| Type | Name | Value  |
| ---- | ---- | ------ |
| A    | api  | VPS_IP |

Proxy: **ON**

## Frontend

Connect domain in **Cloudflare Pages → Custom Domains**.

---

# Enable SSL (HTTPS)

Install Certbot:

```bash
sudo apt install certbot python3-certbot-nginx -y
```

Generate certificate:

```bash
sudo certbot --nginx -d api.clientdomain.com
```

Choose:

```text
Redirect HTTP to HTTPS: Yes
```

Test:

```bash
curl -I https://api.clientdomain.com
```

Expected:

```text
HTTP/2 200
```

---

# Firewall Configuration

```bash
sudo ufw allow OpenSSH
sudo ufw allow 'Nginx Full'
sudo ufw enable
```

Check:

```bash
sudo ufw status
```

---

# File Upload Setup (30–40 GB)

Create upload directory:

```bash
sudo mkdir -p /var/www/uploads
sudo chown -R devi:www-data /var/www/uploads
sudo chmod -R 775 /var/www/uploads
```

Express configuration:

```javascript
app.use('/uploads', express.static('/var/www/uploads'));
```

Uploaded files will be available at:

```text
https://api.clientdomain.com/uploads/file.pdf
```

Check disk usage:

```bash
df -h
du -sh /var/www/uploads
```

---

# Daily Backup Setup

Create backup folder:

```bash
mkdir -p ~/backups
```

Create script:

```bash
nano ~/backup.sh
```

Add:

```bash
#!/bin/bash
tar -czf ~/backups/app-$(date +%F).tar.gz ~/apps/client-project
find ~/backups -type f -mtime +7 -delete
```

Make executable:

```bash
chmod +x ~/backup.sh
```

Add cron job:

```bash
crontab -e
```

Add:

```text
0 2 * * * /home/devi/backup.sh
```

This runs every day at **2:00 AM**.

---

# Monitoring Commands

## Server resources

```bash
htop
free -h
df -h
```

## Nginx logs

```bash
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

## PM2 logs

```bash
pm2 logs client-api
```

## Restart services

```bash
sudo systemctl restart nginx
pm2 restart client-api
```

---

# Deployment Checklist

## Frontend

* [ ] Cloudflare Pages deployment successful
* [ ] Custom domain connected
* [ ] HTTPS working
* [ ] No console errors

## Backend

* [ ] PM2 process online
* [ ] API responding
* [ ] MongoDB connected
* [ ] File upload working

## Security

* [ ] UFW enabled
* [ ] SSL enabled
* [ ] Strong passwords used
* [ ] Recovery email and phone configured

## Backup

* [ ] Backup script created
* [ ] Cron job added
* [ ] Backup files generated

---

# Client Handover Template

## Server Details

* Provider: Hostinger VPS
* OS: Ubuntu 22.04
* IP: xxx.xxx.xxx.xxx

## Domains

* Frontend: https://clientdomain.com
* Backend: https://api.clientdomain.com

## Services

* Nginx
* Node.js
* PM2
* SSL (Let's Encrypt)

## Important Commands

```bash
pm2 status
pm2 restart client-api
sudo systemctl restart nginx
```

## Backup

* Daily backup at 2:00 AM
* Location: /home/devi/backups

## Credentials

Shared separately via secure channel.

---

# Troubleshooting

## Nginx test failed

```bash
sudo nginx -t
```

Fix the syntax error shown.

## PM2 app stopped

```bash
pm2 restart client-api
pm2 logs client-api
```

## Port already in use

```bash
sudo lsof -i :4444
```

Kill the process if needed.

## SSL renewal check

```bash
sudo certbot renew --dry-run
```

---

# Interview Questions

## Q1. Why use a VPS instead of shared hosting?

Because a VPS provides root access, dedicated resources, custom Nginx configuration, and support for Node.js applications and process managers like PM2.

## Q2. Why use PM2?

PM2 keeps Node.js applications running continuously, restarts them automatically on failure, and supports startup on server reboot.

## Q3. Why use Nginx in front of Node.js?

Nginx acts as a reverse proxy, handles HTTPS, serves static files efficiently, and improves security and performance.

## Q4. Why use Cloudflare Pages for frontend?

It provides free static hosting, global CDN, automatic HTTPS, and easy GitHub integration.

## Q5. What is the purpose of Certbot?

Certbot automatically issues and renews Let's Encrypt SSL certificates for HTTPS.

---

# Final Conclusion

For a dedicated client project with a React frontend, Node.js backend, MongoDB database, and 30–40 GB file storage, use:

* Cloudflare Pages (Frontend)
* VPS 2 vCPU / 4 GB RAM / 50 GB SSD (Backend)
* MongoDB Atlas (Database)
* Cloudflare R2 or `/var/www/uploads` (File Storage)
* Nginx + PM2 + SSL (Server stack)

Estimated hosting cost: **₹500–800 per month**.

This setup is secure, scalable, production-ready, and suitable for real client deployments.
