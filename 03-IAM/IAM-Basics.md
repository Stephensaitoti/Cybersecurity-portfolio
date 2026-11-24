# IAM Basics

## 1. What is IAM?

IAM stands for Identity and Access Management. It controls who can sign in to AWS and what they are allowed to do once they are inside. IAM is free, and getting it right matters because many cloud breaches start with stolen or over-powered accounts.
## 2. Users, Groups, Roles and Policies

- *User:* a person or application with its own credentials for signing in to AWS.
- *Group:* a collection of users who share the same permissions, which makes access easier to manage.
- *Role:* a set of temporary permissions that a user or AWS service can assume. It has no long-term password or access keys, so it is safer for applications.
- *Policy:* a JSON document that states which actions are allowed or denied on which resources.
## 3. Least Privilege

Least privilege means giving a user or service only the permissions needed to do its job, and nothing more. For example, someone who only reads reports should not be able to delete data. This limits the damage if an account is ever compromised.
## 4. Root User vs IAM User

The root user is the account owner and has unlimited access to everything in the account. Because it is so powerful, it should be protected with MFA and not used for daily work. Instead, I create an IAM user with only the permissions I need and use that for everyday tasks.
## 5. MFA

Multi-factor authentication (MFA) requires a second proof of identity in addition to a password, such as a code from an authenticator app on my phone. Even if an attacker steals my password, they still cannot sign in without the second factor. MFA is one of the most effective and cheapest security controls in AWS.


## 6. Sample Least-Privilege Policy

json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ReadOnlyOneBucket",
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:ListBucket"],
      "Resource": [
        "arn:aws:s3:::example-portfolio-bucket",
        "arn:aws:s3:::example-portfolio-bucket/*"
      ]
    }
  ]
}


This policy allows only two actions, reading an object and listing a bucket, and only on one bucket. It cannot write or delete data, and it cannot touch any other bucket. That is why it follows least privilege. The bucket name is a made-up example.
## 7. IAM Security Risks
### Risk 1: Compromised Credentials

- Threat: An attacker steals an employee's AWS credentials.
- Vulnerability: No MFA, and permissions broader than the job needs.
- Impact: Unauthorized access to company data and services.
- Recommended control: Enable MFA, apply least privilege, and rotate or remove unused access keys.
- Threat:
- Vulnerability:
- Impact:
- Recommended control:
## 8. Day 4 Reflection

Today I learned how IAM controls who can access AWS and what they can do, and how users, groups, roles and policies fit together. I wrote a sample least-privilege policy and documented how to secure the root user with MFA. I have not created an AWS account yet because I do not have a payment card, so the hands-on setup is the next step once I do.