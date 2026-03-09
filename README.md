# SOC Security Monitoring using Splunk

## Project Overview
This project demonstrates how to build a basic Security Operations Center (SOC) monitoring system using Splunk, Sysmon, and Windows Event Logs.

The objective of this project is to monitor system activity, detect suspicious behavior, and trigger alerts for potential security incidents.

---

## Tools Used

- Splunk Enterprise
- Sysmon
- Windows Event Logs
- Windows 11

---

## Log Sources

The following logs were collected and analyzed:

- Windows Security Logs
- Sysmon Operational Logs

These logs were ingested into Splunk for security monitoring and analysis.

---

## Detection Use Cases

### PowerShell Execution Detection

Detects suspicious PowerShell activity using Sysmon logs.
index=main EventCode=1 Image="*powershell.exe"

---

### Brute Force Login Detection

Detects multiple failed login attempts which may indicate a brute force attack.
index=main EventCode=4625 | stats count by Account_Name, host | where count > 3

---

### Multiple Process Spawn Detection

Detects suspicious processes spawning multiple child processes.
index=main EventCode=1 | stats count by ParentImage | where count > 10

---

## SOC Monitoring Dashboard

A security dashboard was created in Splunk to visualize:

- Failed Login Attempts
- Successful Logins
- PowerShell Execution Activity
- Most Targeted Accounts
- Top Executed Processes

---

## Alerts Configured

The following alerts were created in Splunk:

1. Brute Force Detection Alert
2. PowerShell Execution Detection Alert
3. Multiple Process Spawn Alert

These alerts automatically trigger when suspicious activity is detected.

---

## Conclusion

This project demonstrates how a SIEM platform like Splunk can be used in a SOC environment to collect logs, monitor system activity, detect threats, and generate alerts for security incidents.
