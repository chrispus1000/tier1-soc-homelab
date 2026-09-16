# 🛡️ Tier-1 SOC Analyst Homelab: Wazuh SIEM & Endpoint Detection

## 📖 Overview
This repository documents my personal cybersecurity homelab, designed to simulate the daily workflow of a Tier-1 SOC Analyst. The goal was to build a hybrid environment, generate real-world attack telemetry, and practice incident response and triage using the MITRE ATT&CK framework.

## 🏗️ Architecture
![SOC Homelab Diagram]

*   **Attacker Machine:** Ubuntu Linux (Hydra, Nmap)
*   **Victim Endpoint:** Windows 10/11 (Wazuh Agent + Sysmon)
*   **SIEM Server:** Ubuntu Linux (Wazuh Manager, Indexer, Dashboard)

## 🛠️ Tech Stack & Tools
*   **SIEM:** Wazuh 4.9
*   **Endpoint Telemetry:** Sysmon, Windows Event Logs
*   **Attack Simulation:** Hydra (RDP Brute-force), Nmap (Reconnaissance), EICAR (Malware Test File)
*   **Frameworks:** MITRE ATT&CK

## ⚔️ Attack Simulation & Detection Flow
1.  **Reconnaissance:** Nmap scan from the Ubuntu attacker machine identified open ports (445, 139, 3389) on the Windows endpoint.
2.  **Initial Access Attempt:** Hydra was used to simulate an RDP brute-force attack against the Windows Administrator account.
3.  **Telemetry Generation:** The Windows endpoint generated Event ID 4625 (An account failed to log on) and Sysmon Event ID 1 (Process Creation for suspicious PowerShell execution).
4.  **Detection & Correlation:** The Wazuh SIEM ingested the logs, correlated the failed logons, and triggered alerts mapped to MITRE ATT&CK Credential Access tactics (T1110).

## 🕵️‍♂️ Investigation & Triage (Incident Response)
*See the `/screenshots` folder for the full visual evidence.*
*   **Dashboard Analysis:** Filtered out baseline noise to isolate 2 critical authentication failures.
*   **CLI Investigation:** Utilized terminal commands (`tail -f /var/ossec/logs/alerts/alerts.log` and `grep "Rule: 60122"`) to validate alert generation when the OpenSearch dashboard UI experienced filtering issues.
*   **MITRE Mapping:** Verified the alert mapped to Valid Accounts and Credential Access techniques.

## 📂 Repository Structure
*   `/diagrams` - Architecture diagrams.
*   `/screenshots` - Evidence of attacks, SIEM alerts, and terminal logs.
*   `/configs` - Sanitized Sysmon and Wazuh configuration snippets.

## 🎯 Key Takeaways
*   Learned how to deploy and configure Wazuh agents across Windows and Linux environments.
*   Gained hands-on experience tuning out false positives to identify genuine security incidents.
*   Developed a workflow for triaging alerts using both GUI and CLI tools.

---
*Feel free to reach out if you have any questions or if you are hiring for Tier-1 SOC roles!*
