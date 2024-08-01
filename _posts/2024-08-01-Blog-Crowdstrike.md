# Technical details of the Windows BSOD disaster due to CrowdStrike

**TL;DR**  
CrowdStrike, a popular US cybersecurity company, experienced a significant issue with its Falcon product, leading to widespread Windows systems failures. On July 19, 2024, a patch was rolled out that caused Windows machines to fail during boot, showing the "Blue Screen of Death" (BSOD). IT professionals had to manually boot affected systems into safe mode and remove a problematic channel file to restore functionality.

## About Falcon and EDR

To understand the issue, we need to explore CrowdStrike’s Endpoint Detection and Response (EDR) component within the Falcon Sensor platform.

### What Does Falcon’s EDR Do?

- **Data Collection**: Gathers data from endpoints, including process information, network connections, and file activities.
- **Threat Detection**: Uses advanced analytics, machine learning, and behavioral analysis to detect suspicious activities.
- **Incident Response**: Can automatically isolate affected endpoints, terminate malicious processes, and alert security teams.
- **Forensic Analysis**: Provides tools for investigating incidents and understanding attack vectors.
- **Threat Intelligence Integration**: Integrates with threat intelligence feeds for contextual information on detected threats.

### The Role of the EDR Driver

The Falcon Sensor EDR includes a driver component operating at the kernel level, loaded early in the boot process during the ELAM (Early Launch Anti Malware) phase. This allows the driver to monitor and protect the system from the start.

### How Does the EDR Driver Receive Updates?

Falcon updates are automatically pushed from CrowdStrike’s cloud infrastructure, potentially multiple times a day. This characteristic contributed to the rapid spread of the BSOD issue.

## What Caused the Problem?

A recent update included changes to the sensor’s configuration files, specifically targeting malicious named pipes used in cyberattacks. This update contained a buggy channel file (C-00000291*.sys) with a logic error causing the OS to crash and enter a boot loop.

### Memory Allocation Error

The update led to improper memory management, triggering a PAGE_FAULT_IN_NONPAGED_AREA stop code. This error occurs when accessing a memory page not present in the non-paged area, reserved for critical system components.

### Why Did the Driver Crash Cause BSOD and Boot Loop?

- **Kernel-Level Operations**: Drivers have high privileges and direct access to system resources. Errors can lead to severe consequences.
- **System Stability**: Malfunctioning drivers disrupt OS and hardware communication, leading to instability.
- **Protection Mechanism**: Windows initiates a BSOD to prevent further issues when detecting a critical system fault.

## Misconceptions

Early reports suggested NULL bytes in the channel file caused the issue. CrowdStrike clarified this was not the case.

## Closing Thoughts

The incident raises questions about CrowdStrike's update rollout processes and quality checks. Manual remediation required significant effort, particularly for systems with BitLocker encryption. The disaster affected many businesses, highlighting the need for better preventive measures, such as A/B testing or staggered rollouts, to avoid future incidents.

---
Credit: CrowdStrike
