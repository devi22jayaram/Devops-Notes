# Recommended Architecture for Frontend + Backend + 30–40 GB Storage

## Requirement

* Frontend: React / Vite
* Backend: Node.js + Express
* Forms: Contact / Enquiry forms
* Database: MongoDB
* File Storage: 30–40 GB
* SSL: HTTPS
* Domain: Custom domain
* Goal: Low cost, easy maintenance, production-ready

---

## Recommended Architecture

Frontend (Cloudflare Pages)
|
| HTTPS
|
Backend API (VPS - Nginx + PM2 + Node.js)
|
| MongoDB connection
|
MongoDB Atlas (Form data)
|
| File uploads
|
Cloudflare R2 (30–40 GB storage)

---

## VPS Configuration

| Resource  | Recommended      |
| --------- | ---------------- |
| CPU       | 2 vCPU           |
| RAM       | 4 GB             |
| Storage   | 50 GB SSD        |
| OS        | Ubuntu 22.04 LTS |
| Bandwidth | 1–2 TB           |

### Why 50 GB?

* Ubuntu OS: 8–10 GB
* Logs & backups: 5 GB
* Application code: 1–2 GB
* File uploads: 30–40 GB
* Free space for updates: 5–10 GB

---

## Cost Estimate

| Component               | Cost           |
| ----------------------- | -------------- |
| Cloudflare Pages        | Free           |
| MongoDB Atlas           | Free           |
| Cloudflare R2           | ₹50–150/month  |
| VPS (Hostinger/Hetzner) | ₹450–700/month |
| Domain                  | ₹80–150/month  |

### Total Estimated Cost

**₹600–900 per month**

---

## Why this architecture?

### Frontend on Cloudflare Pages

* Free hosting
* Global CDN
* Automatic HTTPS
* Easy deployment
* No server maintenance

### Backend on VPS

* Full root access
* Nginx reverse proxy
* PM2 process management
* SSL support
* Easy debugging and monitoring

### MongoDB Atlas

* Managed database
* Automatic backups
* Easy scaling
* Free tier available

### Cloudflare R2

* Cheap object storage
* No bandwidth egress charges
* Ideal for images, PDFs, and documents
* Easy integration with Node.js

---

## Deployment Flow

### Frontend

```bash
npm install
npm run build
```

Upload the `dist/` folder to **Cloudflare Pages**.

### Backend

```bash
sudo apt update
sudo apt install nginx nodejs npm

npm install
npm run build

pm2 start dist/index.js --name myapp
pm2 save
```

### Nginx Configuration

```nginx
server {
    server_name api.example.com;

    location / {
        proxy_pass http://127.0.0.1:4444;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

### SSL

```bash
sudo certbot --nginx -d api.example.com
```

---

## Interview Question

### Q: What hosting architecture would you choose for a React frontend, Node.js backend, and 30–40 GB storage?

### Answer

I would use Cloudflare Pages for the React frontend, a VPS with 2 vCPU and 4 GB RAM for the Node.js backend, MongoDB Atlas for storing form submissions, and Cloudflare R2 for 30–40 GB of file storage. This setup is production-ready, cost-effective, scalable, and easy to maintain.

---

## Final Conclusion

For a React frontend, Node.js backend, form handling, and 30–40 GB storage, the recommended setup is:

* Cloudflare Pages (Frontend)
* VPS 2 vCPU / 4 GB RAM / 50 GB SSD (Backend)
* MongoDB Atlas (Database)
* Cloudflare R2 (File Storage)
* Nginx + PM2 + SSL

This architecture supports production workloads and costs approximately **₹600–900 per month**.
