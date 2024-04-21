---
title: Hackviser - HackTRace Walkthrough
date: 2024-04-21
categories: [Hackviser]
tags: [Walkthrough, CTF]
---
![HackTrace](https://github.com/voizok/voizok.github.io/assets/110619000/21d9c9cc-5338-4524-a63b-75ad5aa195ac)

## Make sure you are connected via VPN or HackerBox using the Connect button located in the top right corner

![HackTrace3](https://github.com/voizok/voizok.github.io/assets/110619000/4c321694-6630-4aa1-9c44-8cf080054b4a)

**Task:** Let’s start with Exploring the website

![HackTrace4](https://github.com/voizok/voizok.github.io/assets/110619000/a0d8d40b-b32c-4412-aac0-9c131d1ce14a)


### Q1) What is the IP address of the attacker who targeted the website?

Upon inspecting the webpage, I encountered a 'Not Found' page indicating the website is using Apache.

![HackTrace5](https://github.com/voizok/voizok.github.io/assets/110619000/ae7c59f0-6c94-470c-b9fc-a363d04f2dad)


I accessed Apache logs stored at `/var/log/apache2` and found the `access.log` file. After inspecting it, I discovered the attacker's IP address

![HackTrace6](https://github.com/voizok/voizok.github.io/assets/110619000/2959563a-6774-480d-898e-99d540022b5b)

![HackTrace7](https://github.com/voizok/voizok.github.io/assets/110619000/f725d367-3e31-4543-90e3-e6661b7ddb17)


**Answer: 10.0.0.41**

### 2) What tool did the attacker use for directory scanning?

In the same log, it's evident that the attacker used **gobuster** for directory scanning.

![HackTrace7](https://github.com/voizok/voizok.github.io/assets/110619000/d785c9a5-e0e4-4573-856e-1123c9c022e2)


### 3) What is the name of the file uploaded by the attacker to the system that allows remote computer access via the web?

After scrutinizing the log, I found a GET request indicating the upload of **/upload/shell.php**.

![HackTrace8](https://github.com/voizok/voizok.github.io/assets/110619000/c77db94a-d5df-40e5-a627-b7119ca06acd)


**Answer: Shell.php**


### 4) Which function in the software is responsible for the file upload vulnerability?

Navigating to `/var/www/html`, where the website files reside, I analyzed the `upload.php` code and identified the **uploadFile** function as responsible for the vulnerability.

![HackTrace9](https://github.com/voizok/voizok.github.io/assets/110619000/eff2f885-04ec-4603-8458-398bff74582c)


**Answer: uploadFile**

### 5) Which important file has the attacker stolen from the system by compressing it into a zip file?

While examining the files, I stumbled upon **xdfds.sh**, where the attacker compressed a file into **2023-resume.zip**.

![HackTrace10](https://github.com/voizok/voizok.github.io/assets/110619000/90296e13-fc85-448a-813c-702c537ef749)


**Answer: 2023-resume.zip**

### Which domain did the attacker use to upload the data they accessed?

In the same script, the attacker directed the stolen zip file to **dataprocessingframework.hv**.

![HackTrace11](https://github.com/voizok/voizok.github.io/assets/110619000/758245b5-a7f4-4188-8132-e8ac3bd37679)

**Answer: dataprocessingframework.hv**


Thank you for reading!

*Happy Hacking~*
