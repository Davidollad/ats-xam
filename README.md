# AltSchool Cloud Engineering Second Semester Project

## Project Title: The Future of Tech-Enabled African Solutions

This project was created as part of the AltSchool Cloud Engineering second semester examination to demonstrate practical server provisioning, deployment, and application delivery skills.

---

## 🔧 Project Objective
Provision and configure a Linux-based cloud server running a Node.js application (with a React frontend), served via Nginx as a reverse proxy.

---

## 🧰 Tools & Technologies Used
- AWS EC2 (Ubuntu 22.04)
- Nginx (as reverse proxy)
- Node.js v22.16.0 & npm
- React / Next.js
- Git & GitHub
- Custom domain (via Namecheap)
- Route 53 for DNS Management
- Let’s Encrypt (SSL via Certbot)

---

## 🚀 Steps Taken

### 1. **Provisioning the Server**
- I created a new EC2 instance on AWS (Ubuntu 22.04 LTS).
- I allowed HTTP (80), HTTPS (443), and SSH (22) in the security group.
- Connected using EC2 Instance Connect.

### 2. **Initial Server Setup**
```bash
sudo apt update
sudo apt install nginx -y
```

### 3. **Install Node.js v22**
```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt install -y nodejs
```

### 4. **Domain & DNS Configuration**
- Set up a hosted zone in AWS Route 53.
- Updated the Namecheap nameservers to point to Route 53.
- Created A and CNAME records to route traffic to the EC2 public IP.

### 5. **Cloned & Ran React Project**
```bash
git clone https://github.com/davidollad/mage
cd mage
npm install
npm run build
npm start
```
The app started on: `http://localhost:3000`

### 6. **Configured Nginx as Reverse Proxy**
Edited `/etc/nginx/sites-available/default`:
```nginx
location / {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}
```

Tested and reloaded Nginx:
```bash
sudo nginx -t
sudo systemctl reload nginx
```

### 7. **SSL Setup**
I enabled SSL using Certbot:
```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d yourdomain.com
```

---

## 🌐 Live Demo

- **Public IP**: `http://18.130.189.228`
- **Domain**: `https://oladejo.xyz`

---

## 🖼️ Screenshot

![Screenshot of the deployed landing page](screenshot.png)

---

## 📁 Repository Structure
```
/mage
├── app/
├── components/
├── public/
├── styles/
├── package.json
├── README.md
└── ...
```

---

## ✍️ Author

**David Oladejo**  
Cloud Engineering Student, AltSchool Africa Tinyuka 2024  
GitHub: [@davidollad](https://github.com/davidollad)
