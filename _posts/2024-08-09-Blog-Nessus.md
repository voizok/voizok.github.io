---
title: Scanning and Exploiting Vulnerabilities with Nessus
date: 2024-08-08
categories: [Vulnerability]
tags: [Windows,CrowdStrike,Cybersecurity,BSOD]
---
In this article, I will walk you through the process of setting up Nessus, scanning, and exploiting a target on Proving Grounds Play with it.

## What is Nessus?

Nessus is a vulnerability scanner that can scan and assess the complete attack surface of a target. With Nessus, you can scan a network for potential vulnerabilities and even automatically exploit these discovered vulnerabilities. It supports different types of scans such as Host Scan, Basic Network Scan, Malware Scan, Active Directory Scan, etc. Nessus is an excellent tool for enumerating a target network and discovering potential ways to gain access.

## Setting up Nessus

Nessus can be installed on Windows, Linux, Mac, Docker, and even on a Raspberry Pi! 

> **Note:** Add the installation process here according to your operating system.

On the first launch of Nessus, you need to register for Nessus Essentials to be able to use it for free.
![Nessus Registration](image1.png)

You will then need to submit your name and email to receive an activation code.
![Activation Code](image2.png)

Once the registration process is complete, Nessus will download all the plugins and compile them. This process can take a lot of time—it took me 2 hours! So be patient.

Once the plugins are downloaded and compiled, you will be able to start scanning.

## Scan and Exploit

We will perform our first scan on a machine called "Sumo" from Proving Grounds Play, a free platform offered by Offsec to practice hacking. After signing up on Proving Grounds Play, you can download your universal VPN pack to connect to the PG Play's network and scan the target.

To connect using OpenVPN, use the following command:

```bash
sudo openvpn universal.ovpn
