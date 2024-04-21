---
title: Hackviser - HackTRace Walkthrough
date: 2024-04-21
categories: [Hackviser]
tags: [Walkthrough, CTF]
---

## Make sure you are connected via VPN or HackerBox using the Connect button located in the top right corner

![Connected via VPN or HackerBox](link-to-image)

**Task:** Let’s start with Exploring the website

![Website Exploration](link-to-image)

### Q1) What is the IP address of the attacker who targeted the website?

Upon inspecting the webpage, I encountered a 'Not Found' page indicating the website is using Apache.

![Apache Usage](link-to-image)

I accessed Apache logs stored at `/var/log/apache2` and found the `access.log` file. After inspecting it, I discovered the attacker's IP address: **10.0.0.41**.

![IP Address](link-to-image)

### 2) What tool did the attacker use for directory scanning?

In the same log, it's evident that the attacker used **gobuster** for directory scanning.

![Attacker's Tool](link-to-image)

### 3) What is the name of the file uploaded by the attacker to the system that allows remote computer access via the web?

After scrutinizing the log, I found a GET request indicating the upload of **/upload/shell.php**.

Answer: Shell.php

![Uploaded File](link-to-image)

### 4) Which function in the software is responsible for the file upload vulnerability?

Navigating to `/var/www/html`, where the website files reside, I analyzed the `upload.php` code and identified the **uploadFile** function as responsible for the vulnerability.

![Upload Function](link-to-image)

Answer: uploadFile

### 5) Which important file has the attacker stolen from the system by compressing it into a zip file?

While examining the files, I stumbled upon **xdfds.sh**, where the attacker compressed a file into **2023-resume.zip**.

Answer: 2023-resume.zip

![Stolen File](link-to-image)

### Which domain did the attacker use to upload the data they accessed?

In the same script, the attacker directed the stolen zip file to **dataprocessingframework.hv**.

Answer: dataprocessingframework.hv

![Domain](link-to-image)

Thank you for reading!

*Happy Hacking~*
