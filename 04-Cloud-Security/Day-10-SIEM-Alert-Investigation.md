
# Day 10 – SIEM Alert Investigation

## Organisation
Triple S Technologies

## Analyst Role
Junior SOC Analyst

## 1. Learning Objectives

## 1. Learning Objectives

By completing this SIEM alert investigation, I aimed to:

1. Understand how SIEM systems generate security alerts from predefined detection rules.
2. Investigate repeated failed authentication attempts using Linux command-line tools.
3. Identify affected user accounts, source IP addresses and suspicious login patterns.
4. Analyse authentication timestamps and determine whether detection thresholds have been exceeded.
5. Distinguish suspicious activity from confirmed security incidents.
6. Understand how to assess alert severity and determine appropriate escalation procedures.
7. Document investigation evidence, findings and recommendations in a structured SOC investigation report.

## 2. SIEM Alert Investigation Fundamentals

## 2. SIEM Alert Investigation Fundamentals

### 2.1 What Is a SIEM Alert?

A SIEM alert is a notification generated when a security monitoring system identifies activity that matches a predefined detection rule or suspicious behaviour pattern.

Alerts help SOC analysts identify potential security incidents and investigate them before they cause significant damage.

### 2.2 Common Security Alerts

Examples include:

- Multiple failed login attempts.
- Successful login after repeated authentication failures.
- Login from an unusual geographical location.
- Privilege escalation.
- Suspicious administrative activity.
- Malware detection.
- Unusual outbound network connections.
- Unexpected changes to security configurations.

### 2.3 Alert Severity Levels

**Critical:** Indicates an immediate and potentially severe security threat requiring urgent investigation and response.

**High:** Indicates significant suspicious activity that requires prompt investigation.

**Medium:** Indicates potentially suspicious activity that requires further verification.

**Low:** Indicates activity with limited immediate risk that should still be reviewed.

### 2.4 True Positive and False Positive

**True Positive:** An alert correctly identifies genuinely suspicious or malicious activity.

**False Positive:** An alert incorrectly identifies legitimate activity as suspicious.

**Important:** A triggered alert is not automatic proof of a successful attack. Analysts must investigate and validate the available evidence.

### 2.5 SIEM Investigation Process

1. Receive and acknowledge the alert.
2. Review alert details and detection rules.
3. Identify affected users, systems and source IP addresses.
4. Examine relevant authentication and system logs.
5. Correlate related events.
6. Determine whether the activity is legitimate or suspicious.
7. Assign a preliminary severity level.
8. Document findings and escalate when necessary.

## 3. Security Alert Details

## 3. Security Alert Details

### 3.1 Alert Information

| Field | Details |
|---|---|
| Alert ID | SIEM-2026-010 |
| Alert Name | Multiple Failed Login Attempts |
| Username | finance.admin |
| Source IP | 192.0.2.88 |
| Failed Login Attempts | 8 |
| Time Window | 5 minutes |
| Affected System | FINANCE-SERVER-01 |
| Detection Rule | 5 or more failed logins within 5 minutes |
| Initial Priority | High |

### 3.2 Initial Analyst Observation

The SIEM generated an alert after detecting eight failed authentication attempts associated with the finance.admin account within a five-minute period.

The activity exceeds the configured detection threshold of five failed login attempts.

This pattern may indicate a brute-force attempt, password guessing or legitimate authentication problems.

However, the available alert information does not establish whether an unauthorised person attempted access or whether the account was compromised.

Further investigation of authentication logs is required.

## 4. Investigation Methodology

## 4. Investigation Methodology

### 4.1 Evidence Collection

The investigation will use the synthetic authentication log file to examine the failed login activity associated with finance.admin.

### 4.2 Investigation Procedures

1. Count the total failed authentication attempts.
2. Identify the affected username.
3. Identify the source IP address.
4. Examine the timestamps and frequency of login attempts.
5. Confirm whether all attempts originated from the same source.
6. Search for successful authentication events.
7. Determine whether the activity meets the SIEM detection threshold.

### 4.3 Investigation Principles

- Preserve the original log evidence.
- Use verified evidence rather than assumptions.
- Correlate related security events.
- Distinguish suspicious activity from confirmed compromise.
- Document findings accurately.
- Escalate when additional investigation is required.

## 5. Practical Alert Investigatio

## 5. Practical Alert Investigation

### 5.1 Investigation Environment

The investigation was conducted using a synthetic authentication log file in GitHub Codespaces.

Evidence file: `04-Cloud-Security/day10-authentication-events.log`

Operating environment: Linux terminal.

### 5.2 Count Failed Authentication Attempts

Command used:

`grep -c 'FAILED_LOGIN' 04-Cloud-Security/day10-authentication-events.log`

Output:

`8`

Finding: Eight failed authentication attempts were recorded, exceeding the SIEM detection threshold of five attempts.

### 5.3 Identify the Affected Account

Command used:

`grep -o 'user=[^ ]*' 04-Cloud-Security/day10-authentication-events.log | sort -u`

Output:

`user=finance.admin`

Finding: All recorded failed authentication events targeted the finance.admin account.

### 5.4 Identify the Source IP Address

Command used:

`grep 'FAILED_LOGIN' 04-Cloud-Security/day10-authentication-events.log | sed -E 's/.*src=([^ ]+).*/\1/' | sort -u`

Output:

`192.0.2.88`

Finding: All eight failed authentication attempts originated from the same simulated source IP address.

### 5.5 Analyse the Authentication Timeline

Command used:

`grep 'FAILED_LOGIN' 04-Cloud-Security/day10-authentication-events.log`

Finding:

- First attempt: 09:00:12
- Last attempt: 09:04:30
- Total duration: 4 minutes and 18 seconds.
- Average interval: Approximately 37 seconds.

The relatively consistent intervals may indicate automated password guessing, although automation has not been confirmed.

### 5.6 Search for Successful Authentication

Command used:

`

## 6. Investigation Findings

## 6. Investigation Findings

### 6.1 Authentication Activity

The investigation identified eight failed authentication attempts involving the finance.admin account on FINANCE-SERVER-01.

### 6.2 Source Identification

All eight failed login events originated from the same source IP address:

`192.0.2.88`

This address belongs to a reserved documentation IP range and is used only for this training exercise.

### 6.3 Timeline Analysis

The authentication attempts occurred between 09:00:12 and 09:04:30 on 27 November 2026.

The total investigation window was 4 minutes and 18 seconds.

The repeated attempts occurred at relatively consistent intervals, which may indicate automated password guessing. However, automation has not been confirmed.

### 6.4 Detection Threshold Analysis

The SIEM detection rule triggers when five or more failed login attempts occur within five minutes.

Observed failed attempts: 8

Configured threshold: 5

Threshold exceeded by: 3 attempts.

The alert condition was therefore satisfied.

### 6.5 Successful Authentication Check

A search for SUCCESSFUL_LOGIN events returned no matching records in the supplied training log.

This means the available evidence does not establish a successful authentication following the failed attempts.

### 6.6 Analyst Conclusion

The evidence indicates suspicious repeated authentication activity targeting the finance.admin account.

The activity requires further investigation to determine its source and legitimacy.

There is currently insufficient evidence to confirm account compromise or attribute the activity to a specific attacker.

## 7. Risk Assessment and Escalation

## 7. Risk Assessment and Escalation

### 7.1 Preliminary Severity Assessment

**Severity: Medium**

The activity is classified as Medium because eight failed authentication attempts targeted a privileged-looking account within a short period.

The activity exceeded the SIEM detection threshold and may indicate password guessing or automated authentication attempts.

However, no successful login or confirmed account compromise was identified in the supplied evidence.

### 7.2 Potential Security Risks

- Possible password-guessing activity.
- Potential unauthorised access attempts.
- Risk of account compromise if valid credentials are eventually obtained.
- Potential exposure of sensitive financial systems.

### 7.3 Recommended Response Actions

1. Escalate the alert to a Tier 2 SOC Analyst for further investigation.
2. Verify whether finance.admin is an authorised account and identify its owner.
3. Confirm whether the failed login attempts were expected or legitimate.
4. Review authentication logs for additional activity outside the supplied time window.
5. Check MFA status and authentication controls.
6. Correlate endpoint, firewall and identity-provider logs.
7. Review whether any successful authentication or privilege changes occurred

## 8. Lessons Learned

## 8. Lessons Learned

1. SIEM alerts help SOC analysts identify suspicious security events through predefined detection rules.
2. Multiple failed authentication attempts can indicate password guessing or brute-force activity.
3. Detection thresholds help identify unusual authentication patterns.
4. Investigating timestamps and source IP addresses helps establish relationships between security events.
5. A triggered alert does not automatically confirm a successful attack.
6. Searching for successful authentication events provides additional context during account security investigations.
7. Correlating multiple log sources improves investigation accuracy.
8. Proper documentation and escalation support effective incident response.

## 9. Analyst Reflection

## 9. Analyst Reflection

During this exercise, I investigated a SIEM alert involving repeated failed authentication attempts against the finance.admin account on FINANCE-SERVER-01.

I used Linux commands to count failed login events, identify the affected account and source IP address, examine timestamps and search for successful authentication records.

The investigation confirmed eight failed login attempts within a five-minute detection window, exceeding the configured threshold of five attempts.

No successful login event was found in the supplied synthetic log. The activity was therefore assessed as suspicious and requiring further investigation, rather than confirmed account compromise.

I learned the importance of validating alerts, correlating evidence, assessing severity and escalating suspicious activity appropriately. As a Junior SOC Analyst at Triple S Technologies, I would preserve the evidence, document my findings and refer the alert to a Tier 2 analyst for further investigation.
