# Microsoft Sentinel SOC L1 – Windows Brute Force Detection

## Project Overview

This project demonstrates a Security Operations Centre (SOC) Level 1 monitoring and detection workflow using Microsoft Sentinel to identify and investigate suspicious Windows authentication activity.

The lab focuses on detecting multiple failed Windows login attempts that may indicate a brute-force or password-guessing attack.

### Detection Workflow

Windows Server VM → Windows Security Events → Azure Monitor Agent → Data Collection Rule → Log Analytics Workspace → KQL Investigation → Microsoft Sentinel Analytics Rule → Alert → Sentinel Incident

---

## Project Objectives

- Collect Windows Security Events in Microsoft Azure.
- Monitor Windows authentication activity.
- Investigate failed login attempts using KQL.
- Identify suspicious repeated Event ID 4625 activity.
- Create a Microsoft Sentinel analytics rule for brute-force detection.
- Generate an alert from the detection rule.
- Create and review a Microsoft Sentinel incident.
- Demonstrate a SOC L1 investigation and response workflow.

---

## Lab Architecture

Windows Server VM
      |
 Windows Security Events
      |
      v
Azure Monitor Agent (AMA)
      |
      v
Data Collection Rule (DCR)
      |
      v
Log Analytics Workspace
      |
      v
KQL Investigation
      |
      v
Microsoft Sentinel
      |
      v
Analytics Rule
      |
      v
    Alert
      |
      v
Sentinel Incident
      |
      v
SOC L1 Investigation & Response

## Lab Environment

| Component | Configuration |
| Cloud Platform | Microsoft Azure |
| Resource Group | SOC-Sentinel-Lab |
| Windows Server VM | SOC-Windows-VM |
| Log Analytics Workspace | SOC-Sentinel-LAW |
| Data Collection Rule | SOC-Windows-Security-DCR |
| Monitoring Agent | Azure Monitor Agent (AMA) |
| SIEM | Microsoft Sentinel |
| Detection | Potential Brute Force - Failed Logins |
| Primary Event ID | 4625 - Failed Logon |
| Supporting Event ID | 4624 - Successful Logon |


## 1. Azure Resource Group

The Azure resource group `SOC-Sentinel-Lab` was used to organise the resources required for the SOC monitoring lab.

![Resource Group](screenshots/resource-group-png.png)


## 2. Log Analytics Workspace

The Log Analytics Workspace `SOC-Sentinel-LAW` was used as the central location for collecting and querying Windows security event data.

![Log Analytics Workspace](screenshots/02-log-analytics-workspace-png.png)


## 3. Microsoft Sentinel

Microsoft Sentinel was configured as the cloud-native SIEM for monitoring, detecting, and investigating security events.

![Microsoft Sentinel](screenshots/03-microsoft-sentinel-png.png)


## 4. Windows Server Virtual Machine

The Windows Server virtual machine `SOC-Windows-VM` was used as the primary source of Windows security event logs.

![Windows Server VM](screenshots/04-windows-server-vm-png.png)

## 5. Data Collection Rule

The Data Collection Rule `SOC-Windows-Security-DCR` was configured to collect Windows Security Events through the Azure Monitor Agent and send the data to the Log Analytics Workspace.

![Data Collection Rule](screenshots/05-Data Collection Rule-png.png)

## 6. Windows Security Event ID 4625 – Failed Logon

Event ID 4625 represents a failed Windows logon attempt.

Repeated failed authentication attempts can indicate brute-force or password-guessing activity.

![Windows Security Events](screenshots/06-Windows security Events-png.png)

## 7. Windows Security Event ID 4624 – Successful Logon

Event ID 4624 represents a successful Windows logon.

Successful logon events provide additional authentication context and can help a SOC analyst determine whether successful authentication occurred around suspicious failed-login activity.

![Windows Successful Event](screenshots/Windows Sucessful Event.png)

## 8. KQL Investigation

Kusto Query Language (KQL) was used to investigate Windows authentication events collected in Log Analytics.

The investigation focused on:

- Event ID 4625
- Repeated failed login attempts
- Affected user accounts
- Source information
- Authentication activity patterns

Example KQL query:

```kql
SecurityEvent
| where EventID == 4625
| summarize FailedAttempts = count() by Account, IpAddress
| order by FailedAttempts desc
```

This type of query helps a SOC analyst identify accounts and source addresses associated with repeated failed authentication attempts.


...


## 9. Microsoft Sentinel Analytics Rule

A scheduled analytics rule named **Potential Brute Force - Failed Logins** was created to detect multiple Windows failed-login attempts.

The rule uses KQL-based detection logic to identify suspicious authentication activity and generate security alerts.

![Analytics Rule](screenshots/07-Analytics rule-png.png)


## 10. Alert Generation

After the detection condition was met, Microsoft Sentinel generated an alert named **Potential Brute Force - Failed Logins**.

The alert was classified as **Medium severity** and showed the associated security event.

This demonstrates that the configured analytics rule successfully detected the suspicious authentication activity.

![Alert Generated](screenshots/08-Alert-png.png)

## 11. Microsoft Sentinel Incident

The generated alert was associated with a Microsoft Sentinel incident.

The incident provides the SOC analyst with a centralised location to review and investigate the detected security activity.

![Sentinel Incident](screenshots/09-Incidents-png.png)


## 12. SOC L1 Investigation Workflow

When investigating this type of alert, a SOC L1 analyst would:

1. Review the alert name, severity, and timestamp.
2. Examine the associated Event ID 4625 events.
3. Identify the affected account.
4. Review the source IP or host information.
5. Check for repeated failed authentication attempts.
6. Review Event ID 4624 for successful logons.
7. Determine whether the activity is legitimate or suspicious.
8. Document the investigation findings.
9. Escalate confirmed suspicious activity according to the organisation's incident-response process.

## 13. SOC L1 Response

For confirmed suspicious brute-force activity, an analyst may:

- Escalate the incident to the appropriate security team.
- Recommend account protection or password reset procedures.
- Investigate the source system or IP address.
- Review additional authentication activity.
- Document the evidence and investigation timeline.
- Close the incident when the activity is determined to be benign or the investigation is complete.

## 14. Key Learnings

Through this project, I gained hands-on experience with:

- Microsoft Sentinel
- Log Analytics Workspace
- Azure Monitor Agent
- Data Collection Rules
- Windows Security Events
- Event ID 4625 – Failed Logon
- Event ID 4624 – Successful Logon
- Kusto Query Language (KQL)
- Brute-force detection
- Microsoft Sentinel Analytics Rules
- Security alerts
- Sentinel incidents
- SOC L1 investigation workflow
- Security incident response.

## Author

**Sana Sultana**



