# AWS EC2 Complete Setup Guide (Beginner to Production)

## Project Requirement

* React/Vite frontend
* Node.js + Express backend
* MongoDB database
* File uploads (30–40 GB)
* Custom domain
* HTTPS (SSL)
* Dedicated server for one client

---

# Recommended AWS Configuration

| Component      | Recommended             |
| -------------- | ----------------------- |
| EC2 Type       | t3.small                |
| vCPU           | 2                       |
| RAM            | 2 GB                    |
| Storage        | 50 GB gp3 SSD           |
| OS             | Ubuntu Server 22.04 LTS |
| Region         | ap-south-1 (Mumbai)     |
| Estimated Cost | ₹1200–1800/month        |

> If budget is lower, start with **t3.micro (1 GB RAM)** and upgrade later.

---

# Step 1: Create AWS Account

## Open

https://aws.amazon.com/

## Click

**Create an AWS Account**

## Complete

* Email address
* Password
* AWS account name
* Phone verification
* Debit/Credit card
* Choose **Basic Support (Free)**

After verification, log in to **AWS Management Console**.

---

# Step 2: Launch EC2 Instance

## Search

**EC2**

## Click

**Launch Instance**

---

# Step 3: Configure Instance

## Name

```text
client-production-server
```

## AMI

**Ubuntu Server 22.04 LTS (64-bit)**

## Instance Type

**t3.small**

---

# Step 4: Create Key Pair

## Click

**Create new key pair**

### Key pair name

```text
client-server-key
```

### Type

* RSA
* .pem

## Click Create

A file will download:

```text
client-server-key.pem
```

### Important

Store this file safely. AWS will **not allow you to download it again**.

---

# Step 5: Network Settings

## Create Security Group

Allow:

| Type  | Port | Source   |
| ----- | ---- | -------- |
| SSH   | 22   | My IP    |
| HTTP  | 80   | Anywhere |
| HTTPS | 443  | Anywhere |

---

# Step 6: Configure Storage

Change root volume:

| Size  | Type |
| ----- | ---- |
| 50 GB | gp3  |

Then click **Launch Instance**.

Wait until the instance state becomes **Running**.

---

# Step 7: Get Server IP

Go to:

**EC2 → Instances → Select instance**

Copy:

```text
Public IPv4 address
```

Example:

```text
13.234.120.45
```

---

# Step 8: Connect from Windows

## Move the .pem file

Move it to:

```text
C:\\Users\\YOUR_NAME\\.ssh\\client-server-key.pem
```

## Open PowerShell

Run:

```powershell
ssh -i $HOME/.ssh/client-server-key.pem ubuntu@13.234.120.45
```

First time:

```text
Are you sure you want to continue connecting (yes/no)?
```

Type:

```text
yes
```

You should see:

```text
Welcome to Ubuntu 22.04 LTS
```

---

# Step 9: Update Server

```bash
sudo apt update && sudo apt upgrade -y
```

---

# Step 10: Install Nginx

```bash
sudo apt install nginx -y
```

Enable and start:

```bash
sudo systemctl enable nginx
sudo systemctl start nginx
```

Check:

```bash
sudo systemctl status nginx
```

Open browser:

```text
http://YOUR_SERVER_IP
```

You should see **Welcome to Nginx**.

---

# Step 11: Install Node.js

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

Verify:

```bash
node -v
npm -v
```

---

# Step 12: Install PM2

```bash
sudo npm install -g pm2
```

Verify:

```bash
pm2 -v
```

---

# Step 13: Create Application Folder

```bash
mkdir -p ~/apps/client-project/backend
mkdir -p ~/apps/client-project/frontend
```

---

# Step 14: Upload Backend Code

Use **WinSCP** or **VS Code Remote SSH**.

Upload your backend project into:

```text
/home/ubuntu/apps/client-project/backend
```

---

# Step 15: Configure Backend

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

Check:

```bash
pm2 status
```

---

# Step 16: Configure Nginx Reverse Proxy

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

---

# Step 17: MongoDB Atlas Setup

## Open

https://www.mongodb.com/atlas

## Create Free Cluster

* Region: Mumbai
* Cluster name: clientdb

## Create Database User

Save username and password.

## Network Access

Add:

```text
0.0.0.0/0
```

## Get Connection String

```text
mongodb+srv://username:password@cluster.mongodb.net/clientdb
```

Use it in `.env`.

---

# Step 18: Deploy Frontend

## Build locally

```bash
npm install
npm run build
```

## Option A (Recommended) — Cloudflare Pages

Upload the `dist/` folder.

### Build settings

| Setting          | Value         |
| ---------------- | ------------- |
| Build command    | npm run build |
| Output directory | dist          |

---

# Step 19: Configure Cloudflare Domain

## Add domain to Cloudflare

Change nameservers in your domain provider.

## DNS Records

### Frontend

Cloudflare Pages will create this automatically.

### Backend

| Type | Name | Value         |
| ---- | ---- | ------------- |
| A    | api  | EC2_PUBLIC_IP |

Proxy status: **Proxied (Orange cloud)**

---

# Step 20: Enable HTTPS (SSL)

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
Redirect HTTP to HTTPS: 2
```

Test renewal:

```bash
sudo certbot renew --dry-run
```

---

# Step 21: Configure File Upload Storage

Create upload directory:

```bash
sudo mkdir -p /var/www/uploads
sudo chown -R ubuntu:www-data /var/www/uploads
sudo chmod -R 775 /var/www/uploads
```

Express configuration:

```javascript
app.use('/uploads', express.static('/var/www/uploads'));
```

Files will be available at:

```text
https://api.clientdomain.com/uploads/file.pdf
```

---

# Step 22: Configure Firewall

Ubuntu:

```bash
sudo ufw allow OpenSSH
sudo ufw allow 'Nginx Full'
sudo ufw enable
```

AWS Security Group already allows 22, 80, and 443.

---

# Step 23: Create Daily Backup

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
0 2 * * * /home/ubuntu/backup.sh
```

---

# Step 24: Monitoring Commands

## Server usage

```bash
htop
free -h
df -h
```

## PM2

```bash
pm2 status
pm2 logs client-api
pm2 restart client-api
```

## Nginx

```bash
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

---

# Step 25: Deployment Verification

## Frontend

* [ ] Pages deployment successful
* [ ] Custom domain working
* [ ] HTTPS enabled
* [ ] No console errors

## Backend

* [ ] API responds with 200
* [ ] MongoDB connected
* [ ] Form submission works
* [ ] File upload works

## SSL

* [ ] Browser lock icon visible
* [ ] HTTP redirects to HTTPS

---

# Step 26: Client Handover

## Server Details

* AWS Region: ap-south-1
* EC2 Type: t3.small
* Storage: 50 GB gp3
* OS: Ubuntu 22.04

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

* Daily at 2:00 AM
* Location: /home/ubuntu/backups

## Credentials

Share separately via secure channel.

---

# Troubleshooting

## Nginx config error

```bash
sudo nginx -t
```

## PM2 app crashed

```bash
pm2 logs client-api
pm2 restart client-api
```

## Port already in use

```bash
sudo lsof -i :4444
```

## SSL issue

```bash
sudo certbot renew --dry-run
```

---

# Interview Questions

## Why EC2?

EC2 provides scalable virtual servers with full root access and flexible networking.

## Why Nginx?

Nginx acts as a reverse proxy, handles HTTPS, and improves performance and security.

## Why PM2?

PM2 ensures Node.js applications stay online and restart automatically after crashes or server reboots.

## Why Cloudflare Pages for frontend?

It offers free static hosting, global CDN, automatic HTTPS, and easy GitHub integration.

---

# Cost Estimate

| Component        | Monthly    |
| ---------------- | ---------- |
| EC2 t3.small     | ₹1100–1500 |
| 50 GB gp3        | ₹150–250   |
| Cloudflare Pages | Free       |
| MongoDB Atlas    | Free       |
| Total            | ₹1250–1750 |

---

# Final Conclusion

Use:

* **EC2 t3.small (2 vCPU, 2 GB RAM, 50 GB SSD)**
* **Cloudflare Pages for frontend**
* **Nginx + PM2 for backend**
* **MongoDB Atlas for database**
* **/var/www/uploads for 30–40 GB file storage**
* **Cloudflare DNS + SSL**

This setup is production-ready, secure, scalable, and suitable for dedicated client deployments.
