# Incident Report – SOC Monitoring using Splunk

## Incident Summary

During security monitoring in the Splunk SOC lab environment, multiple failed login attempts were detected on the Windows system. The activity indicated a possible brute-force attack against a user account.

The alert was generated automatically by a detection rule configured in Splunk.

---

## Detection Method

The incident was detected using Windows Security Logs ingested into Splunk.

The following Splunk query was used to identify failed login attempts:
index=main EventCode=4625 | stats count by TargetUserName | where count > 3

This query detects multiple failed authentication attempts targeting the same user account.

---

## Investigation

After the alert was triggered, the logs were analyzed in Splunk to determine the cause of the activity.

Key findings:

- Multiple failed login attempts were recorded in Windows Security Logs.
- Event ID *4625* indicated authentication failures.
- The targeted account was *aksha*.
- The activity was generated intentionally during testing to simulate a brute-force attack.

Additional investigation queries were used to analyze system activity, including:

### PowerShell Execution Detection
index=main EventCode=1 Image="*powershell.exe"

### Process Creation Monitoring
index=main EventCode=1

These logs were generated using *Sysmon*, which provides detailed process monitoring.

---

## Impact Assessment

The activity was part of a controlled lab simulation and did not result in a successful compromise.

However, repeated failed login attempts can indicate a brute-force attack in real-world environments.

If not properly monitored, such activity may lead to unauthorized system access.

---

## Response Actions

The following actions were taken:

- Reviewed authentication logs in Splunk
- Confirmed failed login attempts
- Verified that no successful compromise occurred
- Investigated related system activity using Sysmon logs

---

## Recommendations

To prevent brute-force attacks in production environments, the following security measures are recommended:

- Implement account lockout policies
- Enforce strong password policies
- Monitor authentication logs continuously
- Configure SIEM alerts for repeated login failures

---

## Conclusion

This project demonstrates how Splunk can be used in a SOC environment to monitor security events, detect suspicious activity, and trigger alerts for potential incidents.

By ingesting Windows Security Logs and Sysmon logs into Splunk, security analysts can identify threats such as brute-force attacks and suspicious process executions.

The lab successfully simulated detection, investigation, and documentation of a security incident using a SIEM platform.
