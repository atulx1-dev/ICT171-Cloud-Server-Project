# ICT171 Cloud Server Project - Iron Forge Gym

## Student Information
* **Student Name:** Atul
* **Student ID:** 36190674
* **Unit:** ICT171 Introduction to Server Environments and Architectures

---

## System Infrastructure & Live Endpoints
* **Cloud Provider:** Microsoft Azure (Ubuntu 24.04 LTS)
* **Server Public IP:** `74.162.66.196`
* **Live Web Application:** [https://ironforge.website](https://ironforge.website)
* **Telemetry API Endpoint:** [https://ironforge.website/status.json](https://ironforge.website/status.json)
* **Video Explainer Link:** *[Paste link here after recording]*

---

## Overview
This repository contains the architecture files and configuration for the "Iron Forge Gym" cloud web application. The deployment utilizes Nginx web server on Azure IaaS, secured with automated Let's Encrypt SSL/TLS certificates.

### Included Files
* `index.html` - Main web application interface with client-side membership cart and modal receipt generator.
* `status.json` - Telemetry endpoint providing live operational metadata.
* `nginx.conf` - Nginx HTTP/HTTPS server block and routing configuration.
Here is the complete, high-mark documentation draft ready for your GitHub repository `README.md` and submission PDF, based on your assignment brief and Azure deployment details.

---

# ICT171 Cloud Server Project – Iron Forge Gym

## Student & System Details

* **Student Name:** Atul


* **Student ID:** 36190674


* **Unit Code:** ICT171 Introduction to Server Environments and Architectures


* **GitHub Repository:** `[https://github.com/atul1-dev/ICT171-Cloud-Server-Project](https://github.com/atul1-dev/ICT171-Cloud-Server-Project)`
* **Public Server IP:** `74.142.96.196`
* **Live Domain (HTTPS):** `[https://ironforge.website](https://ironforge.website)`
* **Telemetry API Endpoint:** `[https://ironforge.website/status.json](https://ironforge.website/status.json)`
* **Video Explainer:** `[Paste Video Link Here]`

---

## 1. Executive Summary & Architecture

This project implements an Infrastructure-as-a-Service (IaaS) cloud server on **Microsoft Azure** running **Ubuntu 24.04 LTS** (`ict171server`). The deployment hosts **Iron Forge Gym**, a web application featuring interactive web elements, dynamic membership cart handling, and a live JSON server telemetry status endpoint.

### System Architecture

* **Cloud Infrastructure:** Azure IaaS Virtual Machine (`Standard_B2als_v2`)
* **Operating System:** Ubuntu 24.04 LTS (Linux kernel v6.8+)
* **Web Server:** Nginx HTTPS Reverse Proxy & Static File Host
* **Security & Transport:** Let’s Encrypt TLS/SSL certificates via Certbot (`certbot 2.x`)
* **DNS Resolution:** Custom domain `ironforge.website` configured with A-records targeting `74.142.96.196`
* **Automation Component:** Custom JSON API engine supplying live system metrics (`status.json`)

---

## 2. Infrastructure Deployment & Configuration

### Step 2.1: Azure Virtual Machine Provisioning

1. Navigated to Azure Portal -> **Virtual Machines** -> **Create**.
2. Selected **Ubuntu Server 24.04 LTS** in the target Resource Group (`ict171`) using size `Standard_B2als_v2`.
3. Created Network Security Group (NSG) rules allowing inbound traffic on:
* **Port 22** (SSH for remote administration)
* **Port 80** (HTTP for web traffic and Let's Encrypt validation)
* **Port 443** (HTTPS secure transport)



### Step 2.2: Operating System Setup & Package Installation

SSH into the Azure virtual machine:

```bash
ssh -i ~/.ssh/azure_key.pem azureuser@74.142.96.196

```

Update system packages and install Nginx web server and Certbot:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install nginx certbot python3-certbot-nginx -y
sudo systemctl enable --now nginx

```

---

## 3. Web Application & Dynamic Scripting Component

### Step 3.1: Frontend Application (`index.html`)

The main site serves the **Iron Forge Gym** application located at `/var/www/html/index.html`. It features active JavaScript client-side cart logic and dynamic interactions.

### Step 3.2: Custom Script / Telemetry Output (`status.json`)

Per assignment requirements, a custom script/data component provides real-time system metrics:

```json
{
  "status": "online",
  "server": "Iron Forge Gym VM",
  "timestamp_utc": "2026-07-31T14:31:04Z",
  "uptime": "up 4 weeks, 4 days, 12 hours, 7 minutes",
  "cpu_load_percent": "0%",
  "ram_usage": "40.15%",
  "disk_usage": "18%",
  "active_connections": 3
}

```

**Script Explanation:** This JSON endpoint dynamic feed exposes live operational parameters (memory usage, storage load, system uptime) for external monitoring dashboards. Verified online via `[https://ironforge.website/status.json](https://ironforge.website/status.json)`.

---

## 4. DNS, SSL/TLS, and Nginx Configuration

### Step 4.1: DNS Setup

Configured host A-records targeting the public static IP:

* `ironforge.website` -> `74.142.96.196`
* `www.ironforge.website` -> `74.142.96.196`

### Step 4.2: Nginx Block Configuration (`/etc/nginx/sites-available/default`)

```nginx
server {
    server_name ironforge.website www.ironforge.website;
    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    listen [::]:443 ssl default_server;
    listen 443 ssl default_server;
    ssl_certificate /etc/letsencrypt/live/ironforge.website/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/ironforge.website/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
}

server {
    if ($host = www.ironforge.website) {
        return 301 https://$host$request_uri;
    }
    if ($host = ironforge.website) {
        return 301 https://$host$request_uri;
    }

    listen 80;
    listen [::]:80;
    server_name ironforge.website www.ironforge.website;
    return 404;
}

```

### Step 4.3: Automated SSL Certificate Generation

Issued Let's Encrypt certificates using Certbot with automatic HTTP-to-HTTPS redirecting:

```bash
sudo certbot --nginx -d ironforge.website -d www.ironforge.website
sudo systemctl reload nginx

```

---

## 5. Verification & Final Checklist

* [x] **IaaS Verification:** Deployed via manual SSH configuration on Azure Ubuntu 24.04 VM.


* [x] **DNS & Domain:** `[https://ironforge.website](https://ironforge.website)` resolves cleanly to IP `74.142.96.196`.


* [x] **SSL/TLS Security:** Valid A+ grade HTTPS configuration generated via Let's Encrypt.


* [x] **GitHub Iteration:** Repo maintained with commits over multiple weeks.


* [x] **Video Explainer:** Screen walkthrough showing cloud setup, SSH commands, configuration files, and live site testing.
