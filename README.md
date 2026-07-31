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

📖 Step-by-Step Cloud Deployment & Implementation Guide

This guide is designed to take you from a local application to a fully live, secure cloud-hosted web server on Microsoft Azure. Whether you are deploying an API, a portfolio site, or a custom cybersecurity tool like BreachPoint, these foundational steps apply to almost any web technology stack.


📋 Prerequisites

Before you begin, ensure you have the following ready:

A Cloud Account: An active Microsoft Azure account (such as a Free Tier or Student Account).
Local Terminal: A terminal or command-line interface (Terminal on macOS/Linux, or PowerShell/Git Bash on Windows).
Application Code: A web application code structure ready in a local folder or pushed to a GitHub repository.
Basic CLI Comfort: Familiarity with running basic commands (navigating directories, connecting to remote systems).

Complete Guide: Deploying a Production-Ready WordPress Site on AWS EC2 (Ubuntu 24.04 LTS)
📌 Document Overview

This guide covers the end-to-end setup of a high-performance, secure WordPress web application hosted on Amazon Web Services (AWS) using an Ubuntu Linux instance, Apache web server, MySQL database, and PHP engine (LAMP stack).
🛠️ System Architecture & Prerequisites

Before starting, ensure you have:

    An active AWS Account.

    A registered Domain Name (from Namecheap, Cloudflare, GoDaddy, or AWS Route 53).

    An SSH client (Terminal on Mac/Linux, or PowerShell/PuTTY on Windows).

    [ User Request ] 
       │
       ▼
 [ Domain / DNS ] ──(Ports 80 & 443)──► [ AWS Security Group ]
                                              │
                                              ▼
                                   [ EC2 Instance (Elastic IP) ]
                                              │
                                     ┌────────┴────────┐
                                     ▼                 ▼
                              [ Apache Server ]  [ MySQL DB ]
                                     │
                                     ▼
                              [ WordPress Core ]


Phase 1: AWS EC2 Instance & Networking Setup

In this section, we launch an EC2 virtual machine running Ubuntu 24.04 LTS and attach an Elastic IP address to ensure your server maintains a static IP address across reboots.
Step 1.1: Launching the EC2 Instance

    Log in to your AWS Management Console and navigate to the EC2 Dashboard.

    Click Launch Instance.

    Set the instance details:

        Name: WordPress-Web-Server

        Application and OS Images (AMI): Select Ubuntu, then choose Ubuntu Server 24.04 LTS (64-bit).

        Instance Type: Select t2.micro or t3.micro (Free tier eligible).
