<div align="center">

# B084-WK1-PMX-WINDOWS10-SETUP
This is my repo for the network walks internship program extra project. I was setting up the windows vm, configured the IP address, set up the network to the shared NAT network with Kali and tried to ping the IPs back and forth between the two VMs.

**Building a Windows 10 virtual lab for penetration testing and ethical hacking practice**
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />

---

## 📌 Project Overview

This project focuses on setting up a **Windows 10 virtual machine** using VirtualBox and Kali Linux.

The lab is a step by step process in creating a controlled Windows 10 environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be done without risk to real systems or networks.

The network is built on a private virtual subnet that allows additional machines to be added later for authorized security testing.

---
## 🎯 Objectives

The main objectives of this project are to:

- A working Windows 10 virtual machine inside VirtualBox
- Connect it to the same NAT network as the Kali Linux VM
- Confirm both machines can reach each other and the internet.

---

## 🛡️ Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing, not a live network or a system that is not yours. This lab exists to solve that problem: everything runs inside a virtual machine, cut off from the host network, so tools can be run, scans can be launched, and mistakes can be made without any real-world consequences.

It can be used for activities such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

⚠️ **Important:** Every tool and technique used in this lab is restricted to machines within the lab. Nothing should be pointed at a live system without explicit permission.
---

## ⚙️ Lab Configuration

| 🧩 Component       | ⚙️ Configuration   |
| ------------------ | -----------------   |
| 🖥️ Host OS         | Windows 11         |
| ⚡ Processor       | Intel Core i7      |
| 🧰 Hypervisor      | VirtualBox 7.2.22  |
| 🐉 Security OS     | Kali Linux 2026.2  |
| 🌐 Virtual Network | NAT Network        |
| 🧠 Kali Linux IP   | 10.0.0.2/24        |
| 📡 Windows 10 IP   | 10.0.0.10/24       |
| 🚪 Default Gateway | 10.0.0.1           |
| 🌍 DNS Server      | 8.8.8.8            |

---
# 🪜 Lab Setup Procedure

## Step 1. Install Windows 10 ISO
The Windows 10 VM image is downloaded and imported into VirtualBox, with its network adapter attached to the Nat Network created for the Kali Linux VM.

---
## Step 2. Create a new VM in VirtualBox
Create a new VitualBox named Windows 10-Lab with sufficient and safe amount of memory. Attach the Windows 10 ISO downloaded. Boot the Windows and install it.

---
## Step 3. Set up the Network
A dedicated NAT Network was created in the VirtualBox that allowed future VMs added to communicate within the lab. Attached the Windows 10 network to the NAT Network that the Kali VM uses.

---
## Step 4. Set a Static IP inside Windows
In the Windows VM, under the control panel > Network and Sharing > Change adapter settings, click on properties and select the Internet Protocol Version 4 > properties. Configure the IP Address to be as below:
```
◦ IP address: 10.0.0.10
◦ Subnet mask: 255.255.255.0
◦ Default gateway: 10.0.0.1
◦ Preferred DNS: 8.8.8.8

```
---
## Step 5. Test Connectivity
On the Windows VM, open command prompt and run:
```
ping 10.0.0.2 - should reach the Kali VM
ping 8.8.8.8 - should confirm the internet access
```
On Kali VM
```
ping 10.0.0.10 - this should reach Windows
```
<img width="1128" height="752" alt="Screenshot 2026-10-26 111005" src="https://github.com/user-attachments/assets/7243bc47-66d7-4d49-993f-bf780d1e83b5" />

<img width="1128" height="752" alt="Screenshot 2026-10-26 111106" src="https://github.com/user-attachments/assets/52002039-26c0-49fa-8713-5aab1861d664" />


# 🔎 Lab Verification

| ✅ Test                        | 🧾 Command                      | 🎯 Expected Result              |
| ----------------------------- | ------------------------------- | ------------------------------- |
| 🌐 Check IP address           | `ip a`                          | Correct Kali IP displayed       |
| 📡 Test Kali gateway          | `ping 10.0.0.2`                 | Successful replies              |
| 🌍 Test Internet connectivity | `ping 8.8.8.8`                  | Successful replies              |
| 🔎 Test Windows gateway       | `ping 10.0.0.10`                | Successful replies              |

---

# 🐞 Problems Encountered & Solutions

Documenting problems is an important part of the project.

## Problem 1. Gateway connection from Kali to Windows

Initial ping could not find the Windows gateway and the Destination Host was Unreachable. This was because the Windows Firewall blocks incoming pings by default.
<img width="1128" height="752" alt="Screenshot 2026-10-26 101153" src="https://github.com/user-attachments/assets/d202115c-7528-403d-a055-49d93fffd0f0" />


One workaround used during this lab was:

```command prompt as administrator
netsh advfirewall firewall add rule name="Allow ICMPv4" protocol=icmpv4:8,any dir=in action=allow
```
The connectivity was tested again.

> **Important:** The command run applies to all network profiles and only opens for ping, other services will require added rules for them

---

# 💡 What I Learned

Through this project, I learned how to configure a virtual environment and to ping between two VMs for cybersecurity practice.

The most important concepts I learned include:

### 1. NAT vs NAT Network

A standard NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple VMs connected to the same virtual network to communicate with one another while providing network address translation for external connectivity.

Therefore any consecutive VMs created should have the shared NAT Network configuration so that the can be able to connect. 

### 2. Virtual Machine Networking

I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network configuration affects communication between machines.

### 3. Static IP Configuration

I learned how to configure and verify IPv4 addressing, subnet masks, gateways, and DNS settings in Kali Linux.

### 4. Windows Firewall

I learned that by default the Windows Firewall will block pings unless a rule is added to allow them to pass through.

### 5. Documentation

I learned that documenting commands, configuration, screenshots, problems, and solutions is an important part of a professional cybersecurity project.

---

# 🔐 Security & Ethical Use
This laboratory is intended strictly for education purposes only. All tools and techniques are confined to machines within this lab and are never to be used against systems without explicit permission.

---

# 🔗 Tools & Resources

- **Windows 10 ISO** [(https://www.microsoft.com/en-us/software-download/windows10)](https://www.microsoft.com/en-us/software-download/windows10)

---
# 👤 Author

**Michelle Mungai**\
Cybersecurity Professional B084

LinkedIn: (https://www.linkedin.com/in/michellemungai/)

---

## 📌 Project Information

**Program Name:** Cybersecurity at Networkwalks | **Week:** 01 | **Project:** Cybersecurity & Pentesting Lab Setup | **Repository:** GitHub

