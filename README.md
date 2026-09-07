# 🛡️ Automated Incident Response & Threat Enrichment Pipeline

An automated SOC security pipeline that helps detect suspicious activity, check it against threat intelligence sources, and create a Jira ticket automatically.

The project uses:

* **Splunk Enterprise** – Detects suspicious activity
* **n8n** – Automates the response workflow
* **VirusTotal** – Checks file hashes
* **AbuseIPDB** – Checks suspicious IP addresses
* **Jira Cloud** – Creates incident tickets

---

## 🎯 Project Goal

The main goal of this project is to **automate the first steps of SOC incident investigation**.

Instead of manually checking every alert, the pipeline:

**Detects → Enriches → Analyzes → Creates Ticket**

This can help security analysts save time and respond to alerts faster.

---

## 🏗️ How It Works

### 1. Splunk – Detection

Splunk receives Windows **Sysmon logs**.

The project mainly uses:

* **Event ID 1** – Process Creation
* **Event ID 3** – Network Connection

Splunk searches these logs for suspicious activity.

When a matching event is detected, Splunk sends the alert to n8n through a webhook.

---

### 2. n8n – Automation

n8n receives the alert from Splunk and starts the automated workflow.

It extracts important information such as:

* Hostname
* Username
* Process name
* Command line
* File hash
* IP address

n8n then decides what type of information needs to be checked.

---

### 3. VirusTotal – File Hash Check

If the alert contains a **SHA256 file hash**, n8n sends the hash to the VirusTotal API.

VirusTotal provides information about the reputation of the file.

The result is then added to the incident information.

---

### 4. AbuseIPDB – IP Check

If the alert contains an IP address, n8n sends it to the AbuseIPDB API.

The API provides information about the IP reputation and reported malicious activity.

---

### 5. Jira – Incident Ticket

After the threat intelligence checks are completed, n8n automatically creates a **Jira Cloud ticket**.

The ticket contains useful investigation information such as:

* Incident details
* Host information
* Username
* Process information
* Command line
* File hash
* IP address
* VirusTotal results
* AbuseIPDB results

This gives the SOC analyst a structured alert to investigate.

---

## 🔄 Project Workflow

```text
Windows Endpoint
       ↓
   Sysmon Logs
       ↓
 Splunk Enterprise
       ↓
 Suspicious Activity Detected
       ↓
      Webhook
       ↓
       n8n
       ↓
 ┌─────┴─────┐
 ↓           ↓
VirusTotal  AbuseIPDB
 ↓           ↓
 └─────┬─────┘
       ↓
   Jira Cloud
       ↓
 SOC Analyst
```

----
## 📽️ Project Demo

Watch the complete project demonstration:

**[Loom Video Demo] [https://github.com/munazajamil/Splunk-n8n-SOC-Automation-/blob/main/Loom-Video/Automation%20project%20n8n_Splunk%20demo-compressed.mp4])**

---

## 🛠️ Technologies Used

| Technology        | Purpose                             |
| ----------------- | ----------------------------------- |
| Splunk Enterprise | Log collection and detection        |
| Sysmon            | Windows endpoint monitoring         |
| n8n               | Workflow automation                 |
| VirusTotal        | File hash threat intelligence       |
| AbuseIPDB         | IP reputation checking              |
| Jira Cloud        | Incident ticket management          |
| Docker            | Running n8n and supporting services |

---

## ⚙️ Key Features

* Automated security alert detection
* Sysmon log monitoring
* Automated threat intelligence enrichment
* File hash investigation
* IP reputation checking
* Automatic Jira ticket creation
* Error handling for failed API requests
* Reduced manual SOC investigation work

---

## 🧠 Key Learnings

Through this project, I learned:

* How to work with **Splunk detection queries**
* How to use **Sysmon Event IDs**
* How to create automation workflows using **n8n**
* How to work with **REST APIs**
* How to integrate **VirusTotal and AbuseIPDB**
* How to connect Docker services using `host.docker.internal`
* How to extract useful information from event data
* How to automate Jira incident creation
* How to handle API errors without stopping the entire workflow

---

## 🚀 Future Improvements

Possible improvements for this project include:

* Add more threat intelligence sources
* Add automatic severity classification
* Add email/Slack notifications
* Add more Splunk detection rules
* Add automated response actions
* Add incident prioritization
* Add additional SOC tools and integrations

---

## 📌 Project Summary

This project demonstrates how different security tools can be connected to create an **automated SOC incident triage pipeline**.

Instead of manually investigating every alert, the system automatically collects the alert, enriches it with threat intelligence, and creates a Jira ticket for the analyst.

**Splunk → n8n → Threat Intelligence → Jira**

The project is designed to demonstrate practical skills in **SOC operations, SIEM, threat intelligence, security automation, API integration, and incident response**.
