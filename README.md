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
