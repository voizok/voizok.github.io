---
title: Scanning and Exploiting Vulnerabilities with Nessus
date: 2024-08-09
categories: [Cybersecurity,Vulnerability Assessment,Penetration Testing]
tags: [Nessus,Security Testing,Network Security,Vulnerability Management]
---

In this article, I will walk you through the process of setting up Nessus, scanning, and exploiting a target on Proving Grounds Play.

## What is Nessus?

Nessus is a vulnerability scanner that can scan and assess the complete attack surface of a target. With Nessus, you can scan a network for potential vulnerabilities, and even automatically exploit these discovered vulnerabilities. It supports different types of scans like Host Scan, Basic Network Scan, Malware Scan, Active Directory Scan, etc. It is a great tool for enumerating a target network and discovering potential ways to gain access.

## Setting up Nessus

Nessus can be installed on Windows, Linux, Mac, Docker, and even on a Raspberry Pi!. I prefer using it with Windows

## Step 1: Download Nessus Essentials

- Open a web browser and navigate to the [Tenable website](https://www.tenable.com/products/nessus/nessus-essentials).
- Click on the **“Download Nessus Essentials”** button to initiate the download process.

![Nessus Download](https://cdn.discordapp.com/attachments/1271416908679348307/1271473574066126878/nessus-download-windows.png?ex=66b7778a&is=66b6260a&hm=400f9d585c647b2aac124e15c42021d9c3cf43fe8a381a4356105aed9baf71fb&)

- You will be prompted to create a Tenable account or log in if you already have one. Follow the instructions to complete the registration/login process.
- Once logged in, you will be able to download the Nessus Essentials installer for Windows.

## Step 2: Run the Installer

- Locate the downloaded Nessus Essentials installer file on your Windows system (usually in the “Downloads” folder).
- Double-click on the installer file to launch the installation wizard.
- If prompted by User Account Control (UAC), click **“Yes”** to allow the installer to make changes to your system.
- The installation wizard will guide you through the installation process. Click **“Next”** to proceed.

![Nessus Installer ](https://cdn.discordapp.com/attachments/1271416908679348307/1271475388261859380/nessus-installShield-wizard.png?ex=66b7793b&is=66b627bb&hm=c504eaa4100843f8c7ce7d53aa01919de24dcfac7303754ec5131ac08f08bfc9&)

## Step 3: Accept the License Agreement

- Read the Nessus Essentials License Agreement carefully.
- If you agree to the terms of the license agreement, select the checkbox indicating your acceptance.
- Click **“Next”** to continue with the installation.

![Nessus License](https://cdn.discordapp.com/attachments/1271416908679348307/1271475699630346313/essus-licens-agreement.png?ex=66b77985&is=66b62805&hm=78ec7e3765d617103ac568b173000390a7912510d243df9e0b889ea0828fc63b&)

## Step 4: Choose Installation Directory

- By default, Nessus Essentials will be installed in the `C:\Program Files\Tenable\Nessus` directory.

![Nessus File Location](https://cdn.discordapp.com/attachments/1271416908679348307/1271475920426893454/nessus-destination-folder.png?ex=66b779ba&is=66b6283a&hm=7968218fb2c680c871ce30701e7634470da42cfc4336694ee80481e60643c037&)

- If you wish to change the installation directory, click on the **“Change”** button and select a different location.
- Click **“Next”** to proceed.

## Step 5: Start the Installation

- Review the installation summary to ensure that all settings are correct.
- Click on the **“Install”** button to begin the installation process.

![Nessus Installation](https://cdn.discordapp.com/attachments/1271416908679348307/1271476226384597002/begin-nessus-installation-windows.png?ex=66b77a03&is=66b62883&hm=98a89a8971ab4c85e1ff7c96b86c087bee50662575c592de4bfc5b73d4e20720&)

- The installer will extract and install the necessary files to your system. This may take a few moments to complete.

## Step 6: Complete the Installation

- Once the installation is complete, click on the **“Finish”** button to exit the installer.
- Nessus Essentials is now installed on your Windows system.

## Step 7: Access Nessus Web Interface

- Open a web browser on your Windows system.
- In the address bar, type `https://localhost:8834` and press **Enter**.
- You will be redirected to the Nessus login page.

![Nessus Start](https://cdn.discordapp.com/attachments/1271416908679348307/1271476904360415305/nessus-connect-via-SSL.png?ex=66b77aa4&is=66b62924&hm=3252fea72badd100cc7c53bf5ec57de6e6ceb45b4789266b32053ffe7bed1b2e&)

On the first launch of Nessus, you need to register for Nessus Essentials to be able to use it for free.

![Nessus Registration](https://cdn.discordapp.com/attachments/1271416908679348307/1271466154657054721/b94a49_0e6cff0694f6417a980847fc216b2251mv2.png?ex=66b770a1&is=66b61f21&hm=9793210e0970387c5bc4f5d6b1cd068fb3d719a741d9f824d8f58ced9c72ee7a&)

You will then need to submit your name and email to receive an activation code.

![Activation Code](https://cdn.discordapp.com/attachments/1271416908679348307/1271466215390445640/b94a49_8d73a8d6b45f4ca6b197fb7f4fd86683mv2.png?ex=66b770b0&is=66b61f30&hm=776b1444047a1acd96e16e947211e3d913219bd746cb9cb85e4159334dabccb3&)

Once the registration process is complete, Nessus will download all the plugins and compile them. This is going to take a lot of time - it took me 2 hours! So be patient.

Once the plugins are downloaded and compiled, you will be able to start scanning.

## Scan and Exploit

We will perform our first scan on a machine called "Sumo" from Proving Grounds Play, which is a free platform offered by OffSec to practice hacking. Once you sign up on Proving Grounds Play, you can download your universal VPN pack to connect to the PG Play network and scan the target.

To connect using OpenVPN, use the following command:

```bash
sudo openvpn universal.ovpn
```

![OpenVPN Connection](https://cdn.discordapp.com/attachments/1271416908679348307/1271416932817440768/b94a49_55e57f25421b421f9a215e6c06b33e3emv2.png?ex=66b742ca&is=66b5f14a&hm=5c71b547fa9a34ca57082b6fca1bf2f24e0baea61397399d65a3d5df52848a56&)

Now, create a new "Basic Network Scan" on Nessus, setting the target to the IP address of the "Sumo" machine on PG Play.

![Nessus Scan Setup](https://cdn.discordapp.com/attachments/1271416908679348307/1271416999578439792/b94a49_12ec3008eef64557a7eb83f3893791bdmv2.png?ex=66b742da&is=66b5f15a&hm=053866c4dae487c9e07cb4398781dc9df451e12697660547e785ce05708dfdf2&)

Once the scan is complete, you can see that Nessus was able to find multiple vulnerabilities of different severities.

![Nessus Scan Results](https://media.discordapp.net/attachments/1271416908679348307/1271417046063644682/b94a49_3d7fae4644154950bc0c5c4d2aad787dmv2.png?ex=66b742e5&is=66b5f165&hm=0cbdb9f7be303b3800acf5735f91222399ed1ea3c96452acf76433a05c3220c2&=&format=webp&quality=lossless&width=550&height=255)

We'll focus on the "GNU Bash Environment Variable Handling Code Injection (Shellshock)" vulnerability that Nessus identified.

![Shellshock Vulnerability](https://cdn.discordapp.com/attachments/1271416908679348307/1271417107296550942/b94a49_e269c0a2ae9e4d26a254c922747000d6mv2.png?ex=66b742f4&is=66b5f174&hm=ae580f464e5148dcb1eafca409b18f6e60c2b6fe168755c10cdf4bf5537db035&)

Upon opening the report, you can see that Nessus was actually able to exploit this vulnerability. The report also clearly states the exact malicious request that Nessus sent in order to exploit the vulnerability.

![Nessus Exploit Report](https://cdn.discordapp.com/attachments/1271416908679348307/1271417156600594453/b94a49_0a5295664231410a8cd328d952c9f51bmv2.png?ex=66b742ff&is=66b5f17f&hm=e302a51b0192addcd2ce8f6fedd03c582b05823983b0cf8bad86d4cf50bff747&)

Let's try to replicate this request to see if the exploit is actually working.So i asked ChatGPT to give me a CURL one-liner command based on the HTTP request.

![CURL Command](https://media.discordapp.net/attachments/1271416908679348307/1271417276377202771/b94a49_c9d9540ba35c40ab971d0de371372932mv2.png?ex=66b7431c&is=66b5f19c&hm=1e7b31f141beae6377f229fe512465ba58e2abf9a543d6b7e8be471119f4d892&=&format=webp&quality=lossless)

Upon running this CURL command, I got a response from the target that proves that the exploit worked. The response contains the output of the command injected in the request.

![CURL Response](https://cdn.discordapp.com/attachments/1271416908679348307/1271417356484218893/b94a49_44cc532b00dc491299746ac4e49720aemv2.png?ex=66b7432f&is=66b5f1af&hm=2b78e2abc563dbce14790bf46f3dabf86f34a66ca2a401ff245296e29bbd7413&)

Using this exploit, one can inject and run arbitrary commands on the target and even get reverse shell access on the target by doing so.

So just like that, with Nessus, we were able to scan a target, find potential vulnerabilities, and even get a detailed report on how to exploit one of these vulnerabilities.
