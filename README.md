# Cybersecurity Lab Setup

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/VirtualBox-v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
</p>

---

## Project Overview

For this project I built a small virtual lab to practice cybersecurity and penetration testing without touching my main system or any network I don't own. It runs on VirtualBox, with Kali Linux as the attacker machine.

Everything sits on a private NAT Network, so I can add more virtual machines later and have them all talk to each other in the same subnet.

---

## Objectives

- Install the latest recommended version of VirtualBox
- Set up Kali Linux as the attacking machine
- Create a NAT Network using the 10.0.0.0/24 subnet
- Give Kali a fixed IP address: 10.0.0.2/24
- Enable the shared clipboard and drag and drop between host and VM
- Set up a shared folder between the host and Kali
- Make sure Kali has full Internet access

---

## Lab Architecture

The host machine runs VirtualBox. Inside it, Kali Linux is connected to a private NAT Network (10.0.0.0/24) with the fixed IP 10.0.0.2. The NAT Network gives it Internet access, and any VM added to the same network later will be able to communicate with it.

Kali is the only VM for now.

---

## Setup Procedure

### Step 1. Install 7-Zip

The Kali VM image comes as a .7z archive, so I installed 7-Zip first to be able to extract it.

### Step 2. Install VirtualBox

I downloaded VirtualBox 7.2 from the official site and installed it on my host machine.

### Step 3. Create the NAT Network

In VirtualBox I went to File > Tools > Network > NAT Networks and created a new network with these settings:

```text
Name:        NatNetwork
IPv4 Prefix: 10.0.0.0/24
DHCP:        Enabled
IPv6:        Disabled
```

I used a NAT Network instead of plain NAT because VMs on a NAT Network can reach each other and still get Internet access. With plain NAT every VM is isolated from the others, which wouldn't work for a lab with attacker and target machines.

### Step 4. Import Kali Linux

I downloaded the pre-built Kali VirtualBox image from the official website, extracted it with 7-Zip and imported it into VirtualBox. I gave the VM 2048 MB of RAM and attached its network adapter to the NatNetwork I created in the previous step.

I also enabled the shared clipboard and drag and drop (both bidirectional) in the VM settings.

A shared folder was added as well, so I can move files between my host and Kali.

### Step 5. Set the Kali IP Address

Inside Kali I opened Edit Connections, selected Wired connection 1, and in the IPv4 Settings tab switched the method to Manual with these values:

```text
Address:  10.0.0.2
Netmask:  24
Gateway:  10.0.0.1
DNS:      8.8.8.8
```

Having a fixed IP makes it easier to document the lab and to refer to Kali in later exercises.

---

## Verification

| Test                 | Command                      | Expected result             |
| -------------------- | ---------------------------- | --------------------------- |
| Check IP address     | `ip a`                       | Shows 10.0.0.2/24           |
| Ping the gateway     | `ping 10.0.0.1`              | Replies received            |
| Test Internet access | `ping 8.8.8.8`               | Replies received            |
| Test DNS             | `nslookup networkwalks.com`  | Domain resolves             |
| Check Nmap           | `nmap --version`             | Nmap version is displayed   |
| Check shared folder  | Open the folder inside Kali  | Host files are visible      |

---

## What I Learned

**NAT vs NAT Network.** Plain NAT gives each VM Internet access but keeps them separated. A NAT Network puts them all in one private network where they can talk to each other, which is what I need for a multi-machine lab.

**VM networking.** I got a better understanding of how VirtualBox network adapters work and how the network configuration affects what a VM can reach.

**Static IPs.** I practiced setting an IPv4 address, netmask, gateway and DNS by hand in Kali, and checking that everything works.

**Documentation.** Writing down the commands and taking screenshots as I went made the setup easier to repeat, and it is something I'll keep doing in future projects.

---

## Ethical Use

This lab is for educational purposes only. Only test systems you own or have explicit permission to test.

---

## Tools and Resources

- 7-Zip: https://7-zip.org/download.html
- VirtualBox: https://virtualbox.org/wiki/Downloads
- Kali Linux: https://kali.org/get-kali

---

## Author

**Hans Jherssy Canales Raymundo**

LinkedIn: https://www.linkedin.com/in/hans-jherssy-canales-raymundo-7b9895361/
GitHub: https://github.com/HansCnls

---

Program: Cybersecurity at Networkwalks | Week: 01 | Project: Cybersecurity & Pentesting Lab Setup
