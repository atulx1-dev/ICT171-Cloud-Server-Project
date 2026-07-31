# 🏋️ Iron Forge Gym - Cloud-Hosted Fitness Platform

Iron Forge Gym is a modern, responsive cloud-hosted web platform deployed on **Microsoft Azure** infrastructure. Designed for fitness enthusiasts and gym members, it offers seamless navigation across equipment info, membership plans, class schedules, trainer profiles, and a contact form. Featuring an intuitive frontend design and high-performance server delivery via **nginx**, Iron Forge Gym showcases production-ready web hosting standards.

### 🎓 Academic Info
* **Student Name:** Atul Choudhary
* **Student ID:** 36190674
* **Unit:** ICT171 — Server Environments & Architectures
* **Assignment:** Assignment 3 — Cloud Server Project & Video Explainer

### 📹 Video Explainer
* **Walkthrough Video:** *[Insert Your Video Link Here]*

### ☁️ Cloud Deployment Details
* **Cloud Provider:** Microsoft Azure
* **Region:** UAE North
* **VM Name:** IronForge-VM
* **OS:** Ubuntu Server 24.04 LTS
* **Web Server:** nginx
* **Live Web URL: *https://ironforge.website/*
* **Server Public IP:** `74.162.66.196`
* **SSH Remote User:** *ironforge.website
*

---

### 🛠️ Core Features of Iron Forge Gym
* **Equipment Showcase:** Overview of gym equipment and facilities.
* **Membership Tier Showcase:** Clear visual comparisons of flexible workout packages and perks.
* **Class Schedule:** Interactive weekly schedule for gym classes.
* **Trainer Profiles:** Bios and specialties for gym trainers.
* **Contact Form:** Form for prospective members to get in touch.
* **Responsive Multi-Page Design:** Optimized layout built with modern HTML, CSS, and JavaScript.

---

### 📖 Complete Deployment & Cloud Setup Guide

This section documents the actual workflow used to take the Iron Forge Gym site code and serve it live on Azure.

### 📋 Prerequisites

1. **Azure Account:** Active Azure subscription with permission to create VMs.
2. **Terminal Application:** Local command-line tool (macOS/Linux Terminal or PowerShell/Git Bash on Windows).
3. **Source Files:** The Iron Forge Gym web assets (HTML, CSS, JS, and image directories).
4. **Basic Shell Familiarity:** Ability to run basic terminal commands.

---

### 🛠️ Phase 1: Provisioning the Azure VM

1. **Create the Virtual Machine:**
   * In the Azure Portal, go to **Virtual Machines** → **Create**.
   * Choose **Ubuntu Server 24.04 LTS**.
   * Region: **UAE North**.
   * Size: **B1s / Standard** (1-2 vCPUs, 1-2 GiB RAM is enough for a static site).

2. **Configure Authentication:**
   * Use an SSH key pair (recommended) or password authentication.
   * Save your private key (`.pem`) somewhere safe for terminal connections.

3. **Verify Instance Specs:**

   ```text
   +---------------------------------------+---------------------------------------+
   | 💻 VIRTUAL MACHINE PROPERTIES          | 🌐 NETWORKING DETAILS                  |
   +---------------------------------------+---------------------------------------+
   | Server Name:        IronForge-VM       | Public IP Address:   74.162.66.196     |
   | Operating System:   Ubuntu 24.04 LTS   | Virtual Network:     ironforge-vnet    |
   | Region:             UAE North          |                                        |
   | System Status:      Running / Ready    |                                        |
   +---------------------------------------+---------------------------------------+
   | 🎛️ HARDWARE SPECIFICATIONS              | 💿 STORAGE DETAILS                     |
   +---------------------------------------+---------------------------------------+
   | Instance Size:      B1s / Standard     | System Disk Name:    IronForge_OSDisk  |
   | vCPUs:              1 to 2             | Disk Type:           Standard SSD      |
   | Memory (RAM):       1 GiB - 2 GiB      | Storage Volume:      8 GiB - 30 GiB    |
   +---------------------------------------+---------------------------------------+
   ```

4. **Network Security Group (Firewall) Rules:**

   | Service | Port | Protocol | Action | Purpose |
   |---|---|---|---|---|
   | SSH | 22 | TCP | Allow | Secure command-line access for server management. |
   | HTTP | 80 | TCP | Allow | Standard web requests and domain verification. |
   | HTTPS | 443 | TCP | Allow | Encrypted secure web traffic via TLS/SSL. |

   ⚠️ **Security Tip:** Make sure your NSG rules are saved and applied before testing connectivity.

---

### 🔑 Phase 2: System Access & Hardening

1. **Connect via SSH:**

   ```bash
   ssh <your-username>@74.162.66.196
   ```

   Confirm the fingerprint prompt with `yes` on first connection.

2. **Update System Packages:**

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

---

### 🚀 Phase 3: Web Server Installation (nginx)

1. **Install nginx:**

   ```bash
   sudo apt install nginx -y
   ```

2. **Enable and Start the Service:**

   ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
   sudo systemctl status nginx
   ```

3. Navigate to `http://74.162.66.196` in your browser to confirm the nginx default welcome page loads.

---

### 📂 Phase 4: Deploying Iron Forge Gym Files

1. **SFTP Connection Setup:**
   * Use an SFTP client (FileZilla, WinSCP) or `scp` to connect:

   ```bash
   scp -r ./iron-forge-gym/* <your-username>@74.162.66.196:/var/www/html/
   ```

2. **Directory Ownership Configuration:**

   ```bash
   sudo chown -R $USER:$USER /var/www/html
   ```

3. **Transferring Web Assets:**
   * Remove or back up the default `index.nginx-debian.html`.
   * Copy over `index.html`, plus your equipment, membership, schedule, trainers, and contact pages, along with CSS/JS/image assets.
   * Refresh `http://74.162.66.196` to verify the gym site is live.

---

### 🌐 Phase 5: Domain Name Mapping (Optional)

If you have a domain:

1. Add an **A Record**: Host `@`, Value `74.162.66.196`, TTL Automatic / 1 Hour.
2. Add a **CNAME Record**: Host `www`, Value `@`.
3. Verify resolution:

   ```bash
   ping your-gym-domain.com
   ```

---

### 🔒 Phase 6: Encrypting Web Traffic (HTTPS / SSL)

*(Only applicable once a domain is pointed at the server — Let's Encrypt won't issue certs for a bare IP.)*

1. **Install Certbot for nginx:**

   ```bash
   sudo apt install certbot python3-certbot-nginx -y
   ```

2. **Issue Certificate:**

   ```bash
   sudo certbot --nginx -d your-gym-domain.com -d www.your-gym-domain.com
   ```

3. **Confirm Auto-Renewal:**

   ```bash
   sudo certbot renew --dry-run
   ```

---

### 📸 Screenshots

No terminal screenshots needed — everything below comes from either the **Azure Portal** or your **browser** viewing the live site. Save images into a `screenshots/` folder next to this README, then reference them like this:

```markdown
![Azure VM Overview](screenshots/vm-overview.png)
```

Here's what to capture and where it comes from:

| # | Screenshot | Where to get it | Suggested placement |
|---|---|---|---|
| 1 | Azure VM Overview page (shows name, IP, region, size, OS, status) | Azure Portal → Virtual Machines → IronForge-VM → Overview tab | End of **Phase 1** |
| 2 | Networking / NSG inbound rules (22, 80, 443 visible) | Azure Portal → your VM → Networking tab | End of **Phase 1** |
| 3 | "Connect" blade showing SSH connection details | Azure Portal → your VM → Connect tab | **Phase 2** |
| 4 | Run Command output showing nginx active (substitutes for a terminal screenshot) | Azure Portal → your VM → Operations → Run command → `RunShellScript` → run `systemctl status nginx` → screenshot the output panel | End of **Phase 3** |
| 5 | Browser showing your live homepage | Browser at `http://74.162.66.196` | End of **Phase 4** |
| 6 | Browser showing each inner page (equipment, membership, schedule, trainers, contact) | Browser, one screenshot per page | End of **Phase 4** |
| 7 | DNS A record settings (only if you set up a domain) | Your domain registrar's DNS management panel | **Phase 5** |
| 8 | Browser showing the padlock/HTTPS on your domain (only if applicable) | Browser address bar | End of **Phase 6** |

**Tip on #4:** Azure's **Run command** feature (under your VM → Operations → Run command) lets you execute shell commands and see the output right inside the Azure Portal — no local terminal needed, and it still counts as solid proof the server's actually running nginx. Worth using for any "prove it's working" screenshot instead of SSHing in yourself.

Crop screenshots to just the relevant panel (not your whole desktop) and keep filenames descriptive (`vm-overview.png`, not `Screenshot 2026-07-31.png`) so they're easy to drop into a Word doc or slides too if your assignment needs those.

---

### 🏆 Project Summary

The Iron Forge Gym deployment demonstrates:
* **Infrastructure Provisioning:** Azure VM in UAE North running Ubuntu 24.04 LTS.
* **Web Serving Architecture:** nginx serving static site assets.
* **Secure Deployment Pipeline:** SFTP/SCP file transfer with correct ownership and permissions.
* **Encrypted Transport (optional):** Let's Encrypt/Certbot for HTTPS once a domain is attached.

---

### 👥 Authors & License

**Atul Choudhary** (Student ID: 36190674)

This project is released under the MIT License.
