
# Day 6 – AWS CloudTrail Log Analysis

## Organisation
Triple S Technologies

## Investigation Scenario
The security team has identified unusual activity involving an AWS administrator account.

As a SOC Analyst, my responsibility is to examine the CloudTrail events, identify suspicious activities and recommend appropriate security controls.

## 1. Investigation Objectives

- Identify who performed the AWS activities.
- Determine which API actions were performed.
- Identify suspicious activities.
- Examine event timestamps and source IP addresses.
- Recommend security improvements.

## 2. CloudTrail Event Analysis


### Event 1: Successful Console Login
- Time: 08:15 UTC
- User: admin-user
- Source IP: 198.51.100.23
- Action: ConsoleLogin
- Result: Success
- MFA: No

Observation: A successful administrator login occurred without MFA being recorded.

### Event 2: Failed Console Login
- Time: 08:20 UTC
- User: admin-user
- Source IP: 203.0.113.77
- Action: ConsoleLogin
- Result: Failure

Observation: A failed login attempt occurred from a different IP address.

### Event 3: Access Key Creation
- Time: 08:22 UTC
- User: admin-user
- Source IP: 203.0.113.77
- Action: CreateAccessKey

Observation: An access key creation event was recorded. Further investigation is needed to establish whether the operation succeeded.

### Event 4: Administrator Policy Attachment
- Time: 08:25 UTC
- User: admin-user
- Source IP: 203.0.113.77
- Action: AttachUserPolicy
- Policy: AdministratorAccess

Observation: An event attempting to attach a highly privileged administrator policy was recorded. Its success and target user must be verified.


## 3. Suspicious Activity Identification

## 3. Suspicious Activity Identification

### Finding 1: Successful Login Without MFA
- Time: 08:15 UTC
- User: admin-user
- Source IP: 198.51.100.23
- Event: ConsoleLogin
- Result: Success
- MFA: No

Security concern:
The administrator successfully accessed the AWS account without MFA being recorded.

### Finding 2: Failed Login Attempt
- Time: 08:20 UTC
- User: admin-user
- Source IP: 203.0.113.77
- Event: ConsoleLogin
- Result: Failure

Security concern:
A failed login attempt occurred from a different source IP address.

### Finding 3: Access Key Creation
- Time: 08:22 UTC
- User: admin-user
- Source IP: 203.0.113.77
- Event: CreateAccessKey

Security concern:
An access key creation event occurred from the same IP address as the failed login.

### Finding 4: Administrator Policy Attachment
- Time: 08:25 UTC
- User: admin-user
- Source IP: 203.0.113.77
- Event: AttachUserPolicy
- Policy: AdministratorAccess

Security concern:
An event attempting to attach a highly privileged administrator policy was recorded.

## 4. Investigation Findings


## 4. Investigation Findings

The investigation identified a sequence of potentially suspicious AWS activities involving the IAM identity admin-user.

The key observations were:

1. A successful console login occurred without MFA being recorded.
2. A failed console login followed from a different source IP address.
3. An access key creation event was recorded from the same IP address as the failed login.
4. An event attempting to attach the AdministratorAccess policy was recorded shortly afterwards.

The repeated use of source IP address 203.0.113.77 for the final three events is an important correlation point.

### Risk Assessment

Severity: HIGH – Pending verification.

Reason:
The combination of failed authentication, access key creation and an AdministratorAccess policy attachment presents a potentially serious account compromise and privilege escalation scenario.

Investigation status: Further verification required.

The available synthetic logs do not independently establish that an attacker successfully compromised the account.


## 5. Security Recommendations


## 5. Security Recommendations

1. Enforce MFA for all privileged IAM identities.
2. Investigate the source IP address associated with the suspicious activities.
3. Verify whether the access key was successfully created and identify its owner.
4. Verify whether AdministratorAccess was successfully attached and identify the target user.
5. Review IAM permissions and remove unauthorised privileges.
6. Investigate CloudTrail records for additional suspicious activities.
7. Rotate or deactivate compromised access keys where compromise is confirmed.
8. Review account activity and strengthen access monitoring.

All containment actions should be performed by authorised security personnel following incident response procedures.


## 6. Analyst Conclusion


## 6. Analyst Conclusion

The investigation identified potentially suspicious AWS account activity involving the admin-user identity.

The sequence of events included a successful login without MFA being recorded, a subsequent failed login, access key creation and an attempt to attach the AdministratorAccess policy.

These activities may indicate attempted account compromise and privilege escalation.

Further investigation is necessary to confirm whether the operations succeeded and whether they were authorised.

As a SOC Analyst, I recommend verifying the affected IAM resources, reviewing additional CloudTrail records, enforcing MFA and applying the principle of least privilege.

This investigation demonstrates the importance of continuous cloud activity monitoring and timely security incident response.

