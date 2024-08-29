---
title: Mastering SOC and Splunk: Real-Time Threat Detection and Response
description: This blog explores the critical role of Security Operations Centers (SOC) in real-time threat detection and response, highlighting key functions like monitoring, investigation, and response. It also demonstrates how Splunk enhances SOC capabilities with powerful data analytics, log management, and alerting features to protect against cyber threats.
date: 2024-08-29
categories:
  - Cybersecurity
tags:
  - Security Operations Center (SOC)
  - Threat Detection
  - Log Management
  - SIEM
image:
  path: thbnls/splunk_soc.png
---

In today's digital landscape, the importance of a robust cybersecurity framework cannot be overstated. Organizations worldwide are constantly under threat from cyberattacks, making the role of Security Operations Centers (SOC) and tools like Splunk pivotal in safeguarding critical assets. This blog explores the fundamental aspects of SOC, its components, and how Splunk plays a crucial role in monitoring and responding to security incidents.

#### What is a Security Operations Center (SOC)?

A Security Operations Center (SOC) is a centralized unit within an organization responsible for monitoring, detecting, investigating, and responding to cyber threats in real-time. The SOC is the frontline defense, ensuring that an organization’s data, intellectual property, and overall cybersecurity posture are protected 24/7.

**Key Functions of a SOC:**
1. **Prevention and Detection**: SOC teams continuously monitor networks to identify potential threats and mitigate them before any damage occurs. This proactive approach is crucial in preventing cyberattacks.
2. **Investigation**: When suspicious activity is detected, SOC analysts conduct thorough investigations to understand the nature and scope of the threat.
3. **Response**: Once a threat is confirmed, the SOC coordinates an immediate response, including isolating endpoints, terminating harmful processes, and restoring systems to their pre-incident state.

#### Components of a SOC

A well-structured SOC comprises several key components:

1. **Security Information and Event Management (SIEM)**: A SIEM system is at the heart of a SOC, collecting and analyzing security event data from various sources. It helps identify potential security incidents and alerts SOC analysts.
2. **Incident Response Plan**: This plan outlines the steps to be taken during a security breach, detailing the roles and responsibilities of the SOC team.
3. **Threat Intelligence**: SOC teams leverage threat intelligence to stay informed about the latest cyber threats and trends, enabling them to take proactive security measures.
4. **Security Analytics**: Analyzing data to identify patterns and anomalies is crucial in detecting potential security threats.
5. **Forensics**: In the event of a security incident, digital forensics helps in collecting and analyzing data to identify the root cause and gather evidence.
6. **Vulnerability Management**: Regularly identifying and addressing security vulnerabilities is essential in maintaining a secure infrastructure.
7. **Threat Hunting**: Proactively searching for potential security threats that may not have been detected by automated tools.
8. **Reporting and Communication**: Effective communication of security incidents to senior management and stakeholders is vital for transparency and accountability.

#### The Role of Splunk in SOC Operations

Splunk is a powerful platform used in SOCs for searching, analyzing, and visualizing machine-generated data. It plays a critical role in log management and triggering alerts in response to security events.

**Key Features of Splunk:**
1. **Data Collection and Indexing**: Splunk collects data from a variety of sources, making it easier to monitor and analyze security events.
2. **Search Language**: Splunk’s search language allows for complex queries, enabling SOC teams to filter and correlate data effectively.
3. **Data Visualization**: Splunk’s customizable dashboards and charts help visualize data trends, making it easier to spot anomalies.
4. **Alerting and Notifications**: Splunk can be configured to send alerts in real-time when specific conditions are met, ensuring that SOC teams can respond swiftly to potential threats.

#### Practical: Log Management and Triggered Alerts in Splunk

One practical example of Splunk in action is its use in monitoring logs and triggering alerts for failed login attempts or brute force attacks.

**Collecting Logs From Kali Linux To Splunk**

Here’s a step-by-step guide on how to set up and configure Splunk on Ubuntu:

## Configuring Splunk Forwarder on Ubuntu

Setting up a Splunk forwarder on Ubuntu involves several key steps. Follow this guide to ensure proper configuration and connection with your Splunk instance.

### 1. Login to Ubuntu
Start by logging into your Ubuntu system. You can do this either through the graphical user interface or via SSH if you're working remotely.

### 2. Open the Terminal
Once logged in, open the terminal application. You can do this by searching for "Terminal" in your application menu or using the shortcut `Ctrl + Alt + T`.

### 3. Check the Present Working Directory
To ensure you’re in the correct directory, use the `pwd` command to print your working directory. If you’re currently on the Desktop and need to navigate to `/opt`, use the following command:

```bash
cd /opt
```
 ### 4. List Directory Contents
Check the contents of the `/opt` directory to locate the Splunk forwarder folder:

```bash
ls
```
### 5. Navigate to the Splunk Forwarder Directory
Once you’ve located the Splunk forwarder directory, change to that directory using:

```bash
cd "Splunk forwarder"
```
### 6. List the Contents of the Splunk Forwarder Directory
To view the contents of the Splunk forwarder directory, use:

```bash
ls
```
### 7. Change Directory to `bin`
Next, navigate to the `bin` directory within the Splunk forwarder folder:

```bash
cd bin
```
### 8. Connect Splunk Forwarder to Your Splunk Instance

To connect the Splunk forwarder to your Splunk instance, use the following command. Replace `(windows Ip)` with the IP address of your Splunk instance:

```bash
sudo ./splunk add forward-server (windows Ip):9998
```
### 9. Restart Splunk

Finally, restart Splunk to apply the changes:

```bash
sudo ./splunk restart
```

image_url:

Then start the Splunk enterprise to check whether the log is collected or not. Start the Splunk enterprise and select search and reporting then select data summary there we can see the log of the event.

Image_url:

# Checking Failed Login Attempts in Splunk

After setting up the Splunk forwarder, follow these steps to check if failed login attempts are logged:

## 1. Open a New Terminal
- Open a new terminal in Ubuntu.

## 2. Login via SSH
- Change the directory if needed.
- Use the SSH command to connect to your Kali Linux machine:

     ```bash
     ssh (username)@(Kali Linux ip)
     ```
- Enter an incorrect password to simulate a failed login attempt.

## 3. Search for Logs in Splunk
- Go to your Splunk web interface.
- Search for failed login logs using this query:
     ```spl
     host="Kali" "failed password" ssh2
     ```
 - You should see the log entry for the failed login attempt.

Image_uri :

Next we need to set the alert for the failed logins and Brute forcing. Select alert from the dropdown list of save as option. Then change the alert settings

image_uri:

Here’s a straightforward guide for setting up and testing alerts for brute force attacks in Splunk:

image_uri:

## Kali Brute Force Alert Setup and Testing

### 1. Configure the Brute Force Alert
1. **Create a New Alert**
   - Title: `Kali Brute Force`
   - Alert Type: `Real-Time`
   - Severity: `High`
   - Save the alert.

2. **Check Triggered Alerts**
   - Go to the `Activity` option in Splunk.
   - Select `Triggered Alerts`.
   - Look for the alert corresponding to the failed login attempts.

### 2. Test Brute Force Attack
1. **Brute Force Kali Linux**
   - Use the following command to perform a brute force attack on Kali Linux:
   - 
     ```bash
     hydra -l (username) -P /usr/share/wordlists/file.txt (Kali Linux IP) ssh
	```
   
   - Replace `(username)` with the target username and `(Kali Linux IP)` with the IP address of the Kali Linux machine.

2. **Brute Force Ubuntu**
   - To brute force Ubuntu, use:
   - 
     ```bash
     hydra -l (username) -P /usr/share/wordlists/file.txt (Kali Linux IP) ssh
     ```
   
   - Replace `(username)` with the target username and `(Kali Linux IP)` with the IP address of the Ubuntu machine.

### 3. Verify Alerts
- Check Splunk to ensure that the brute force alert has been triggered and is visible in the `Triggered Alerts`.

image:


Then check the Splunk enterprise for the alert of the brute forcing.Then check the Splunk enterprise for the alert of the brute forcing.

image :


Splunk’s ability to trigger alerts in response to specific events, such as failed login attempts or brute force attacks, is a crucial feature for SOC teams. These alerts allow for immediate action, minimizing the impact of potential security breaches.

#### Conclusion

In conclusion, the Security Operations Center is a critical component of an organization’s cybersecurity strategy, providing continuous monitoring and protection against cyber threats. Tools like Splunk enhance the capabilities of SOC teams, enabling them to respond effectively to security incidents. By understanding and implementing the key components of a SOC and leveraging platforms like Splunk, organizations can significantly improve their security posture and resilience against cyberattacks.
