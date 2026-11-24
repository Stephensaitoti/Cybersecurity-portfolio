
# AWS Cloud Security Foundations

**Student:** Stephen Saitoti Sankau  
**Learning Path:** AWS Cybersecurity  
**Day:** 1  
**Date:** 23 November 2026

## 1. Introduction to Cloud Computing

Cloud computing is the delivery of computing services over the internet. These services include servers, storage, databases, networking, and software.

Organizations use cloud computing to reduce infrastructure costs, improve scalability, and access computing resources when needed.

## 2. Cloud Service Models

### Infrastructure as a Service (IaaS)
Provides virtualized computing resources such as servers, storage, and networking.

Example: Amazon EC2.

### Platform as a Service (PaaS)
Provides a platform for developers to build, deploy, and manage applications without managing all the underlying infrastructure.

Example: AWS Elastic Beanstalk.

### Software as a Service (SaaS)
Provides ready-to-use software applications over the internet.

Example: Gmail.

## 3. AWS Global Infrastructure

### AWS Regions
Geographical areas where AWS operates its cloud infrastructure.

### Availability Zones
Isolated locations within an AWS Region, consisting of one or more data centres.

### Edge Locations
Locations used by AWS services such as CloudFront to deliver content closer to users.

## 4. AWS Shared Responsibility Model

AWS is responsible for security OF the cloud.

Customers are responsible for security IN the cloud.

Examples of AWS responsibilities:
- Physical data centre security.
- Hardware maintenance.
- Underlying cloud infrastructure.

Examples of customer responsibilities:
- Managing user permissions.
- Protecting sensitive information.
- Configuring network security.
- Managing access credentials.

## 5. Common Cloud Security Risks

1. Weak passwords and stolen credentials.
2. Publicly exposed storage.
3. Excessive user permissions.
4. Poor security monitoring.
5. Unencrypted sensitive information.

## 6. Security Controls

- Multi-Factor Authentication (MFA).
- Least Privilege Access.
- Encryption.
- Security monitoring and logging.
- Regular access reviews.

## 7. Day 1 Reflection

Today I learned the fundamentals of cloud computing, AWS global infrastructure, cloud service models, and the AWS Shared Responsibility Model.

These concepts provide the foundation for understanding cloud security operations and governance, risk, and compliance.

## 8. Practical Exercise: Amazon S3 Security Risk Assessment

**Organisation:** Triple S Technologies

**Scenario:** The organisation stores confidential customer records in an Amazon S3 bucket.

### Risk 1: Unauthorised Public Access

- Threat: An attacker accesses confidential customer records.
- Vulnerability: Incorrect S3 bucket permissions.
- Impact: Exposure of confidential information.
- Recommended control: Enable S3 Block Public Access and review bucket policies.
- Responsibility: Customer.

### Risk 2: Compromised User Credentials

- Threat: An attacker steals an employee's AWS credentials.
- Vulnerability: Weak authentication and excessive permissions.
- Impact: Unauthorised access to company data.
- Recommended control: Enable MFA and apply least privilege.
- Responsibility: Customer.

### Risk 3: Data Exposure

- Threat: Confidential information is exposed.
- Vulnerability: Inadequate data protection.
- Impact: Privacy breaches and reputational damage.
- Recommended control: Apply appropriate encryption and access controls.
- Responsibility: Customer.

### Security Analyst Reflection

As a junior Cloud Security Analyst, I have learned that securing an S3 bucket requires correctly configured permissions, strong authentication, encryption, and continuous monitoring.
