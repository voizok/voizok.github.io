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

Nessus can be installed on Windows, Linux, Mac, Docker, and even on a Raspberry Pi!

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
Let's try to replicate this request to see if the exploit is actually working.

I asked ChatGPT to give me a CURL one-liner command based on the HTTP request.

![CURL Command](https://media.discordapp.net/attachments/1271416908679348307/1271417276377202771/b94a49_c9d9540ba35c40ab971d0de371372932mv2.png?ex=66b7431c&is=66b5f19c&hm=1e7b31f141beae6377f229fe512465ba58e2abf9a543d6b7e8be471119f4d892&=&format=webp&quality=lossless)
Upon running this CURL command, I got a response from the target that proves that the exploit worked. The response contains the output of the command injected in the request.

![CURL Response](https://cdn.discordapp.com/attachments/1271416908679348307/1271417356484218893/b94a49_44cc532b00dc491299746ac4e49720aemv2.png?ex=66b7432f&is=66b5f1af&hm=2b78e2abc563dbce14790bf46f3dabf86f34a66ca2a401ff245296e29bbd7413&)
Using this exploit, one can inject and run arbitrary commands on the target and even get reverse shell access on the target by doing so.

So just like that, with Nessus, we were able to scan a target, find potential vulnerabilities, and even get a detailed report on how to exploit one of these vulnerabilities.
