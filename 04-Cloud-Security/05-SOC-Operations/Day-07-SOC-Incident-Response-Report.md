
# Day 7 – SOC Incident Response Report

## Organisation
Triple S Technologies

## Analyst Role
Junior SOC Analyst

## 1. Executive Summary


Triple S Technologies conducted a simulated AWS security investigation involving potentially suspicious IAM activity.

The investigation examined four synthetic CloudTrail events involving an IAM identity named admin-user.

The observed activities included a successful console login without MFA, a failed login from a different source IP address, an access key creation event, and an AdministratorAccess policy attachment event.

The event sequence raised concerns about possible unauthorised access, credential misuse and privilege escalation.

The investigation identified a potentially high-risk security scenario requiring further verification, evidence preservation and appropriate incident response measures.

No actual AWS compromise was established. The investigation used synthetic log records and documentation-only IP addresses.


## 2. Investigation Scope

The investigation focused on four synthetic AWS CloudTrail events recorded between 08:15 UTC and 08:25 UTC.

The review examined:

- The IAM identity associated with the events: admin-user.
- Console login activity and MFA information.
- Source IP addresses associated with the recorded events.
- The CreateAccessKey event.
- The AttachUserPolicy event involving the AdministratorAccess policy.

The investigation was limited to the supplied sample JSON records. No live AWS environment was accessed, and no real user accounts or infrastructure were investigated.

The source IP addresses are reserved documentation addresses used for testing and do not identify real attackers.

## 3. Evidence and Event Timeline

### Evidence Source

The primary evidence source was the synthetic CloudTrail event file:

`sample-cloudtrail-events.json`

The file contains four events associated with the IAM identity `admin-user`.

### Event Timeline (UTC)

| Time (UTC) | Event | Source IP | Observation |
|---|---|---|---|
| 08:15 | ConsoleLogin – Success | 198.51.100.23 | Successful login; MFA not used |
| 08:20 | ConsoleLogin – Failure | 203.0.113.77 | Failed login attempt |
| 08:22 | CreateAccessKey | 203.0.113.77 | Access key creation event recorded |
| 08:25 | AttachUserPolicy | 203.0.113.77 | AdministratorAccess policy attachment event recorded |

### Evidence Observations

- The first login was successful but did not use MFA.
- A failed login was recorded five minutes later from a different IP address.
- Two potentially sensitive IAM management events followed from the second IP address.
- The sequence warrants investigation, but it does not prove that the failed login caused the subsequent API activity.
- The available records do not confirm whether the access key creation or policy attachment succeeded.

**Evidence limitation:** The IP addresses are reserved documentation addresses, and all events are synthetic training data.

## 4. Suspicious Activity Findings

### 1. Successful Login Without MFA

The admin-user identity recorded a successful console login at 08:15 UTC from 198.51.100.23 without MFA.

This creates a security concern because administrative accounts should use multi-factor authentication.

### 2. Unusual Login Activity

At 08:20 UTC, a failed console login was recorded from 203.0.113.77.

The change in source IP address within five minutes of the successful login warrants further investigation.

### 3. Potential Credential Persistence

At 08:22 UTC, a CreateAccessKey event was recorded under the admin-user identity.

Unauthorised creation of access keys could allow continued access to AWS resources.

### 4. Potential Privilege Escalation

At 08:25 UTC, an AttachUserPolicy event referencing AdministratorAccess was recorded.

If unauthorised and successful, this action could grant excessive administrative permissions to the affected IAM user.

### Overall Assessment

The sequence of events presents indicators of potentially suspicious IAM activity.

However, the available evidence does not confirm a successful compromise, establish the target of the policy attachment, or prove that the API operations succeeded. Further investigation is required.

## 5. Risk Assessment

### Risk Evaluation

**Likelihood: High (Provisional)**

The unusual sequence of login and IAM management events suggests a potentially serious security issue. However, the available synthetic evidence does not confirm unauthorised access.

**Potential Business Impact: Critical**

If the IAM activities were unauthorised and successful, an attacker could potentially create credentials, obtain excessive permissions, access sensitive resources, or disrupt business operations.

**Initial Risk Severity: High**

The incident is provisionally classified as High because of the potential impact of administrative account misuse.

### Risk Treatment

- Escalate the incident to the SOC Team Leader.
- Preserve the original CloudTrail evidence.
- Verify the API operation outcomes and affected IAM resources.
- Investigate the legitimacy of the login and IAM changes.
- Apply appropriate containment measures if unauthorised activity is confirmed.

### Risk Assessment Limitation

This is a preliminary assessment based on synthetic events. The severity must be reviewed when additional evidence becomes available.

## 6. Incident Response Recommendations

### 1. Preserve Evidence

- Preserve the original CloudTrail JSON records.
- Record event timestamps, event names, source IP addresses and user identities.
- Maintain an investigation timeline.
- Restrict access to the evidence to authorised personnel.

### 2. Verify Suspicious IAM Activities

- Inspect the complete CloudTrail event records.
- Check responseElements, requestParameters, errorCode and errorMessage.
- Verify whether the access key was successfully created.
- Identify the actual target of the AdministratorAccess policy attachment.
- Confirm whether the activities were authorised.

### 3. Contain Confirmed Threats

If unauthorised activity is confirmed:

- Deactivate confirmed compromised access keys.
- Remove unauthorised administrative permissions.
- Review and revoke affected sessions using appropriate AWS procedures.
- Coordinate containment actions with the incident response team.

### 4. Strengthen Account Security

- Enforce MFA for all privileged IAM identities.
- Apply least-privilege access policies.
- Review IAM users, roles and access keys.
- Enable continuous monitoring of suspicious account activity.

### 5. Document and Escalate

- Record investigation findings in the incident ticket.
- Notify the SOC Team Leader.
- Document all containment decisions and supporting evidence.
- Reassess incident severity as additional evidence becomes available.

## 7. Evidence Limitations

### Investigation Limitations

1. **Synthetic Data:** The investigation used simulated CloudTrail events rather than records from a live AWS environment.

2. **Documentation IP Addresses:** The addresses 198.51.100.23 and 203.0.113.77 are reserved for documentation and do not identify real attackers.

3. **Unconfirmed API Outcomes:** The available records do not conclusively establish whether the CreateAccessKey and AttachUserPolicy operations succeeded.

4. **Unknown Policy Target:** The available evidence does not establish which IAM user received the AdministratorAccess policy.

5. **Unverified Attribution:** The sequence of events does not prove that the failed login caused the subsequent IAM management activities.

6. **Limited Investigation Scope:** No live IAM resources, access keys, user sessions or AWS account configurations were available for verification.

### Conclusion on Evidence Reliability

The evidence is suitable for a simulated SOC investigation and demonstrates suspicious activity patterns. However, additional CloudTrail records and IAM configuration evidence would be required to confirm an actual security incident.

## 8. Final Analyst Conclusion

The investigation identified a sequence of potentially suspicious AWS IAM activities involving the admin-user identity.

The key observations included a successful console login without MFA, a failed login from a different source IP address, an access key creation event and an AdministratorAccess policy attachment event.

These activities indicate a potentially high-risk security scenario involving possible credential misuse and privilege escalation.

The recommended response is to preserve the evidence, verify the outcomes of the IAM operations, investigate whether the activities were authorised and apply appropriate containment measures if unauthorised activity is confirmed.

The investigation did not establish an actual AWS compromise because the records were synthetic and the outcomes of the API operations were not independently verified.

As a SOC Analyst, I recommend continued investigation and escalation to the SOC Team Leader until the suspicious activities are resolved.

## 9. Lessons Learned

### Key Lessons

1. **MFA Is Essential:** Privileged IAM accounts should always use multi-factor authentication to reduce the risk of unauthorised access.

2. **Continuous Monitoring:** CloudTrail logs provide valuable visibility into AWS account activity and help analysts investigate suspicious events.

3. **Least Privilege:** Administrative permissions should only be granted when necessary and must be regularly reviewed.

4. **Credential Management:** IAM access key creation and usage should be monitored to identify potentially unauthorised credentials.

5. **Evidence-Based Investigation:** SOC analysts must verify event details and operation outcomes before declaring a security breach.

6. **Incident Response:** Early detection, evidence preservation, appropriate containment and clear escalation are essential for effective incident handling.

### Personal Reflection

This investigation improved my understanding of AWS CloudTrail analysis, suspicious IAM activity identification, preliminary risk assessment and incident response documentation.

I also learned the importance of distinguishing suspicious indicators from confirmed security incidents.