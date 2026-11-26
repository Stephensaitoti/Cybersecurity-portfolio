# Day 5 – AWS Cloud Security Controls

## Organisation
Triple S Technologies

## 1. Encryption at Rest


Encryption at rest protects stored information from unauthorised access by encrypting data while it is saved on storage systems.

In AWS, services such as Amazon S3 and Amazon EBS support encryption at rest.

For Triple S Technologies, customer documents stored in an S3 bucket should be encrypted to reduce the risk of sensitive information being exposed if unauthorised access occurs.


## 2. Encryption in Transit


Encryption in transit protects information while it travels between systems over a network.

HTTPS uses Transport Layer Security (TLS) to encrypt communication between a customer's browser and a web application.

For Triple S Technologies, HTTPS should be enforced on its website to protect customer information, login credentials and other sensitive data during transmission.

This helps reduce the risk of data interception and tampering during communication.


## 3. AWS KMS


AWS Key Management Service (KMS) is a managed AWS service that helps create, manage and control cryptographic keys.

These keys are used to encrypt and decrypt sensitive information.

For Triple S Technologies, AWS KMS can help manage encryption keys used to protect customer documents stored in Amazon S3.

Access to encryption keys should be restricted to authorised users and services using appropriate permissions.


## 4. Multi-Factor Authentication


Multi-Factor Authentication (MFA) is a security mechanism that requires users to provide more than one verification factor when accessing an account.

Examples include:
- Something you know: Password.
- Something you have: Authenticator app or security key.
- Something you are: Biometric verification.

For Triple S Technologies, all privileged AWS accounts should use MFA to reduce the risk of unauthorised access if passwords are compromised.

Phishing-resistant security keys should be preferred where supported.


## 5. Least Privilege


The Principle of Least Privilege means giving users and services only the permissions required to perform their assigned responsibilities.

For Triple S Technologies:
- Finance employees should only access authorised financial reports.
- Developers should access only the resources required for development.
- Security analysts should access relevant security logs.
- Administrator permissions should be restricted to authorised personnel.

Regular access reviews should be conducted to identify and remove unnecessary permissions.

This reduces the risk of unauthorised access and limits the potential impact of compromised accounts.


## 6. Security Monitoring


Security monitoring helps organisations identify suspicious activities, investigate security incidents and maintain visibility into their cloud environments.

### AWS CloudTrail
Records AWS account activities, including API calls made by users, roles and services.

### Amazon GuardDuty
Detects potential threats and suspicious activities in AWS environments.

### AWS Security Hub
Provides a central view of security findings and helps assess the security posture of an AWS environment.

For Triple S Technologies, these services can support security monitoring, threat detection and incident investigation.


## 7. Security Recommendations


Triple S Technologies should implement the following security controls:

1. Enable MFA for all privileged accounts.
2. Apply least privilege to IAM users and roles.
3. Encrypt sensitive information at rest and in transit.
4. Enable appropriate AWS CloudTrail logging and regularly review security events.
5. Monitor potential threats using Amazon GuardDuty and review findings through AWS Security Hub.

These controls help reduce unauthorised access, improve threat detection and strengthen the organisation's cloud security posture.


## 8. Analyst Reflection


An attacker who obtains an AWS administrator's password may gain unauthorised access to sensitive cloud resources if additional security controls are not in place.

Without Multi-Factor Authentication (MFA), the attacker may be able to access the administrator's account using the stolen password alone.

This could lead to:
- Unauthorised access to sensitive customer information.
- Modification or deletion of important cloud resources.
- Exposure of encryption keys and confidential data, depending on permissions.
- Disruption of business operations.
- Financial and reputational damage.

As a cybersecurity analyst, I recommend enabling MFA, enforcing least privilege, monitoring account activity through AWS CloudTrail, and investigating suspicious activities using Amazon GuardDuty.

Regular IAM permission reviews and security assessments should also be conducted to reduce the risk of account compromise.
