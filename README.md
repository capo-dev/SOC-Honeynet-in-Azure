# Building a SOC + Honeynet using Azure

![Project Layout](image_link_here)  <!-- Replace with your actual image URL -->

## 🚀 Project Introduction

In this project, I built a **mini honeynet** in **Azure** to simulate an insecure environment and analyze security activity. The primary goal was to **ingest log data** from various sources into a **Log Analytics workspace**, which was then processed by **Microsoft Sentinel** to:

- **Build attack maps**
- **Trigger alerts**
- **Create incidents** based on security events

### 🕵️‍♂️ Experiment Breakdown

The experiment was conducted in two stages over **48 hours**:

- **Stage 1**: Measured key security metrics in an **insecure environment** for **24 hours**.
- **Stage 2**: Applied **security controls** to harden the environment and measured the same metrics for another **24 hours**.

By comparing the metrics from both stages, I was able to evaluate the effectiveness of the security controls applied.

### 📊 Key Metrics Monitored

- **SecurityEvent** (Windows Event Logs) – Logs of critical **Windows security events**.
- **Syslog** (Linux Event Logs) – Logs from **Linux systems** to identify potential security threats.
- **SecurityAlert** (Log Analytics Alerts) – Alerts triggered by **Microsoft Sentinel** based on detected patterns.
- **SecurityIncident** (Incidents created by Sentinel) – Security incidents automatically created in Sentinel from observed attacks.
- **AzureNetworkAnalytics_CL** (Malicious Flows) – Data on **malicious network traffic** attempting to access the honeynet.

---

This experiment helped me assess the impact of security controls on improving the overall security posture of the environment and mitigating threats effectively.

# Architecture Before Hardening / Security Controls

![ab1](https://github.com/user-attachments/assets/902dcdbf-5596-46da-a502-7cdb9d32dec1)

# 🛡️ Architecture After Hardening / Security Controls

![Architecture Layout](image_link_here) 

The architecture of the mini honeynet in **Azure** consists of the following components:

### 🏗️ Core Components:
- **Virtual Network (VNet)**
- **Network Security Group (NSG)**
- **Virtual Machines** (2 Windows, 1 Linux)
- **Log Analytics Workspace**
- **Azure Key Vault**
- **Azure Storage Account**
- **Microsoft Sentinel**

## 🌐 **Before Hardening / Security Controls**
Prior to applying security measures, the architecture was exposed to the internet, with the following configuration:
- All resources were publicly accessible, with **no use of Private Endpoints**.
- **Virtual Machines** had their **Network Security Groups** and built-in firewalls **wide open**, exposing them to potential threats.
- Other resources such as **Azure Key Vault** and **Storage Account** also had **public endpoints** visible to the internet.

## 🔒 **After Hardening / Security Controls**
After implementing security controls, the architecture was modified as follows:
- **Network Security Groups (NSGs)** were hardened by **blocking all traffic**, except for traffic from my **admin workstation**.
- All resources were **protected by built-in firewalls**.
- **Private Endpoints** were introduced for sensitive resources, such as **Azure Key Vault** and **Azure Storage Account**, reducing the exposure to the public internet.

---

This architecture hardening significantly improves the security posture of the environment by limiting unnecessary exposure and enhancing protection against potential attacks.

# Attack Maps Before Hardening / Security Controls

### 🗺️ MySQL:
![MySQL BEFORE](https://github.com/user-attachments/assets/978a4bce-a04a-456e-a750-0b12e3a97246)

### 🗺️ NSG:
![NSG BEFORE](https://github.com/user-attachments/assets/22c8dee8-f841-4533-9b6d-ce9f6a69e9ea)

### 🗺️ Linux SSH:
![Linux SSH auth BEFORE](https://github.com/user-attachments/assets/0083be5d-3f0c-496b-a215-26dce55ac069)

### 🗺️ Windows RDP:
![Windows RDP BEFORE](https://github.com/user-attachments/assets/c01042a4-7f3f-4174-a9ad-39f1a917de63)

# Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

| **Metric**        | **Count** |
|-------------------|-----------|
| **SecurityEvent**  | 19470     |
| **Syslog**         | 3028      |
| **SecurityAlert**  | 10        |
| **SecurityIncident** | 348    |

*Start Time*: 2023-03-15 17:04:29  
*Stop Time*: 2023-03-16 17:04:29 (REPLACE WITH CORRECT TIME STAMPS)

---

# Attack Maps After Hardening / Security Controls

All map queries actually returned **no results** due to **no instances of malicious activity** for the 24-hour period after hardening.

# Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:

| **Metric**             | **Count** |
|------------------------|-----------|
| **SecurityEvent**       | 8778      |
| **Syslog**              | 25        |
| **SecurityAlert**       | 0         |
| **SecurityIncident**    | 0         |
| **AzureNetworkAnalytics_CL** | 0 |
| **AzureNetworkAnalytics_CL** | 843 |

*Start Time*: 2023-03-18 15:37  
*Stop Time*: 2023-03-19 15:37 (REPLACE WITH CORRECT TIME STAMPS)

---

# Conclusion

In this project, a mini honeynet was constructed in **Microsoft Azure** and log sources were integrated into a **Log Analytics workspace**. **Microsoft Sentinel** was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. 

It is noteworthy that the number of **security events** and **incidents** were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the **24-hour period** following the implementation of the security controls.
