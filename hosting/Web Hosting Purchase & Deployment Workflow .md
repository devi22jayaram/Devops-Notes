# Web Hosting Purchase & Deployment Workflow (DevOps)

## Scenario

Client requests:

> "Please purchase web hosting and deploy my website."

As a DevOps Engineer, follow the workflow below.

---

# Step 1: Gather Client Requirements

Before purchasing hosting, collect the following information:

- Domain name (Already purchased or not?)
- Website type
  - React / Vite
  - HTML/CSS
  - WordPress
  - PHP
- Number of websites
- Email hosting required?
- Backend hosting required?
- Expected monthly traffic
- Storage requirement

**Example Questions**

- Do you already own the domain?
- What technology is your website built with?
- Do you need business email?
- Will the backend run on a separate server?

---

# Step 2: Select the Appropriate Hosting Plan

Choose the hosting based on the application.

| Website Type | Recommended Hosting |
|--------------|--------------------|
| HTML | Shared Hosting |
| React / Vite | Shared Hosting |
| WordPress | WordPress Hosting |
| PHP | Shared Hosting |
| Node.js Backend | VPS |
| High Traffic Application | VPS / Cloud Server |

---

# Step 3: Recommend a Hosting Plan

Example:

Hostinger Unlimited Web Hosting

Features:

- 50 GB NVMe Storage
- Unlimited Websites
- Free SSL
- Daily Backups
- CDN
- Free Domain (1 Year)

---

# Step 4: Obtain Client Approval

Never purchase hosting without client approval.

Share:

- Plan Name
- Cost
- Duration
- Features

Example:

Hostinger Unlimited Web Hosting

Cost:
₹9,552 (4 Years)

Equivalent:
₹199/month

Includes:

- 50 GB Storage
- Unlimited Websites
- SSL
- Daily Backups
- CDN

---

# Step 5: Purchase Hosting

Best Practice:

Always purchase hosting using the client's own hosting account.

Reason:

- Client owns the hosting.
- Easier future maintenance.
- Easier ownership transfer.

---

# Step 6: Access the Hosting Control Panel

After purchasing:

Hosting
→ Manage

Available Options:

- File Manager
- Domains
- SSL
- DNS
- Email
- Databases
- Backups

---

# Step 7: Connect the Domain

If the domain is already registered:

Update:

- Nameservers

OR

- DNS Records

Wait for DNS propagation.

Typical propagation time:

5 minutes to 48 hours

---

# Step 8: Build the Frontend Project

React/Vite

```bash
npm install
npm run build
```

Output Folder

Vite

```
dist/
```

React

```
build/
```

---

# Step 9: Deploy the Website

Open:

Hosting
→ File Manager
→ public_html

Upload:

- dist/
OR
- build/

Delete the default Hostinger page before uploading.

---

# Step 10: Enable SSL

Hosting

↓

SSL

↓

Install

Verify:

https://example.com

---

# Step 11: Verify Website

Check:

- Website loads successfully
- HTTPS works
- Images load
- CSS loads
- JavaScript loads
- API calls work correctly
- Browser Console has no errors
- Mobile responsiveness

---

# Step 12: Handover to Client

Provide:

- Hosting Login
- Domain Details
- Renewal Date
- Hosting Plan Details
- Deployment Information

---

# Complete Workflow

Client Requirement
        │
        ▼
Collect Requirements
        │
        ▼
Choose Hosting
        │
        ▼
Get Client Approval
        │
        ▼
Purchase Hosting
        │
        ▼
Access Hosting Panel
        │
        ▼
Configure Domain
        │
        ▼
Wait for DNS
        │
        ▼
Build Project
        │
        ▼
Upload Files
        │
        ▼
Enable SSL
        │
        ▼
Test Website
        │
        ▼
Handover to Client

---

# DevOps Best Practices

✔ Purchase hosting using the client's account.

✔ Store hosting credentials securely.

✔ Enable SSL before making the website live.

✔ Keep a backup before every deployment.

✔ Verify DNS propagation.

✔ Test the website after deployment.

✔ Document all deployment details.

---

# Interview Questions

## Q1. What information do you collect before purchasing web hosting?

Answer:

- Domain details
- Website technology
- Traffic estimation
- Storage requirement
- Email requirement
- Backend hosting requirement

---

## Q2. Why should hosting be purchased in the client's account?

Answer:

Purchasing hosting in the client's account ensures that the client owns the hosting service, making future maintenance, renewals, and ownership transfers easier while avoiding dependency on the developer.

---

## Q3. When should Shared Hosting be used instead of VPS?

Answer:

Shared Hosting is suitable for static websites, React applications, HTML websites, WordPress, and low-to-medium traffic applications.

VPS is recommended for backend applications, Node.js servers, Docker containers, custom software, and high-traffic applications.

---

## Key Takeaways

- Understand client requirements before purchasing hosting.
- Select the hosting plan based on the application.
- Obtain client approval before payment.
- Purchase hosting using the client's account.
- Configure the domain and deploy the application.
- Enable SSL and verify the deployment.
- Hand over credentials and deployment documentation to the client.
