
# AWS Global Infrastructure

**Student:** Stephen Saitoti Sankau
**Learning Path:** AWS Cybersecurity
**Day:** 2
**Topic:** AWS Global Infrastructure

## 1. AWS Regions

An AWS Region is a separate geographical area where AWS operates its cloud infrastructure.

Examples:
- US East (N. Virginia): us-east-1
- Europe (Ireland): eu-west-1
- Africa (Cape Town): af-south-1

Security considerations:
- Data residency
- Regulatory compliance
- Disaster recovery
- Service availability

## 2. Availability Zones

An Availability Zone is an isolated location within an AWS Region, consisting of one or more data centres.

Benefits:
- High availability
- Fault tolerance
- Infrastructure resilience

Security considerations:
- Access control
- Data protection
- Backup and recovery
- Monitoring

## 3. Edge Locations

Edge Locations are AWS points of presence used to deliver content closer to end users.

Example service: Amazon CloudFront.

Security considerations:
- DDoS protection
- Secure content delivery
- Web application protection

## 4. Practical Architecture Scenario

Organisation: Triple S Technologies

The organisation wants to host a secure web application using AWS.

Proposed architecture:
- Route 53 for DNS.
- CloudFront for content delivery.
- An Application Load Balancer for application traffic.
- EC2 instances deployed across two Availability Zones.
- Amazon S3 for object storage.

## 5. Security Recommendations

1. Apply least privilege to IAM users and roles.
2. Use MFA for privileged access.
3. Restrict network access using security groups.
4. Enable encryption for sensitive data.
5. Monitor activity using AWS CloudTrail.
6. Design for resilience across multiple Availability Zones.

## 6. Day 2 Reflection

Today I learned how AWS Regions, Availability Zones and Edge Locations work together.

I also learned how infrastructure design contributes to availability, resilience and cloud security.