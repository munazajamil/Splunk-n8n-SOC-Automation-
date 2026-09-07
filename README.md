# 🛡️ Automated Incident Response & Threat Enrichment Pipeline

An automated Security Operations Center (SOC) incident triage pipeline built with **Splunk Enterprise**, **n8n**, **VirusTotal**, **AbuseIPDB**, and **Jira Cloud**. 

This system ingests Sysmon endpoint logs, enriches detected process/network telemetry with external threat intelligence in real time, and automatically opens triage tickets on a Jira board to reduce Mean Time to Respond (MTTR).

---

## 📽️ Project Demo & Walkthrough

[Watch the Loom Video Demo Here]([[_LOOM_VIDEO_LINK_](https://github.com/munazajamil/Splunk-n8n-SOC-Automation-/tree/main/Loom-Video)]

---

## 🏗️ Architecture & Execution Flow

1. **Detection (Splunk Enterprise):** Splunk ingests Windows Sysmon logs (`EventCode 1` for Process Creation, `EventCode 3` for Network Connections) and triggers real-time webhooks upon detecting suspicious command execution.
2. **Orchestration (n8n):** Receives the HTTP POST webhook payload from Splunk via `host.docker.internal` and applies conditional routing logic:
   - **File Hashes (SHA256):** Queried against the **VirusTotal v3 REST API**.
   - **IP Addresses:** Queried against the **AbuseIPDB API**.
3. **Resilience & Handling:** Error handling (`Continue on Error`) prevents pipeline failure if a hash is unknown (404) or an API rate limit is reached.
4. **Ticketing (Jira Cloud):** Creates structured, actionable tickets containing user context, process details, host information, and reputation scores.

---

## ⚙️ Key Learnings
- Container-to-container network routing in Docker using `host.docker.internal`.
- Parsing unformatted XML event data using Regex and expressions in n8n.
- Ensuring pipeline stability with node-level error tolerance.

  Linkedin: linkedin.com/in/munazajamil
