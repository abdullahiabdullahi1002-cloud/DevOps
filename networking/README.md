# AbdullahiNetworks  
**NGINX Website on AWS EC2 with Cloudflare Integration**

## Project Overview  
AbdullahiNetworks is a lightweight web server deployment using Amazon EC2 and NGINX, with domain and DNS management via Cloudflare. This project outlines a reliable and cost-effective setup suitable for small to medium-sized web applications or personal projects.

## Objective  
To provide a simple, secure, and reproducible process for deploying a cloud-based web server using EC2, with NGINX handling web traffic and Cloudflare managing DNS.

## Key Features  
- **Domain Integration** – e.g., AbdullahiNetworks.com  
- **Cloud Hosting**
- **Secure Access**
- **NGINX Web Server**
- **DNS via Cloudflare**

## Technologies Used  
- Amazon EC2  
- NGINX  
- Cloudflare DNS  
- SSH  

---

## Deployment Guide

### 1. Register a Domain  
- Purchase a custom domain (e.g., AbdullahiNetworks.com).

### 2. Launch EC2 Instance  
- Select Amazon Linux 64-bit (Free Tier eligible)  
- Instance type: `t3.micro`  
- Name the instance: `AbdullahiNetworks`
<img width="1928" height="1000" alt="Pasted Graphic 1" src="https://github.com/user-attachments/assets/dece67c0-b4d8-460b-93f5-b5f4c8a51746" />


### 3. Create SSH Key Pair  
- Generate a key pair (e.g., `private-key.pem`)  
- Download and store it securely  

### 4. Configure Security Groups  
- **SSH (Port 22)** – Source: your IP only  
- **HTTP (Port 80)** – Source: Anywhere
<img width="1841" height="925" alt="Pasted Graphic 3" src="https://github.com/user-attachments/assets/741f5433-a83b-4fd3-b5a0-407e947eecbb" />
  
### 5. Connect via SSH

```bash
chmod 400 private-key.pem
ssh -i private-key.pem ec2-user@[Your-EC2-Public-IP]
```

## Configure DNS with Cloudflare

### Steps:
1. Log in to Cloudflare  
2. Add your domain (e.g., AbdullahiNetworks.com)  
3. Update nameservers at your domain registrar to the ones provided by Cloudflare  
4. In Cloudflare DNS settings, add an A record:  
   - Name: `nginx` (for `nginx.yourdomain.com`) 
   - Point to your EC2 public IPv4 address  
   - Set proxy status to **DNS only** (gray cloud)   
<img width="1710" height="1107" alt="Pasted Graphic 5" src="https://github.com/user-attachments/assets/803ee564-02dc-4732-b834-6d620df89507" />

---

## Note on DNS Setup

This configuration uses Cloudflare. With Cloudflare, you update your domain’s nameservers at your registrar to Cloudflare, then point your DNS records to your EC2 instance’s public IP. With Route 53, if your domain is registered in AWS, DNS is managed automatically, and you create records pointing to your EC2 IP without changing nameservers.

---

## Verification

Visit your domain (e.g., `nginx.abdullahinetworks.com`) — you should see the default NGINX welcome page.
<img width="3420" height="2214" alt="image" src="https://github.com/user-attachments/assets/9164bb32-7337-48f8-b9d6-df460bc3f657" />


---

## Security Best Practice

Never open SSH to 0.0.0.0/0 because it exposes your server to everyone. Limit SSH access to your IP to keep it secure.

---
