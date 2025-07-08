# Infrastructure as a Service (IaaS) Security

## What is IaaS?
IaaS provides virtual computing infrastructure managed over the internet (e.g., AWS EC2, Azure VM).

## Security Considerations

### 1. Shared Responsibility Model
- **Cloud Provider:** Secures physical infrastructure, hypervisors, and hardware.
- **You (Customer):** Secure OS, software, network configuration, and data.

### 2. Common Risks
- Misconfigured storage (e.g., open S3 buckets)
- Weak IAM policies or leaked credentials
- No network segmentation

### 3. Best Practices

#### a. Identity and Access Management (IAM)
- Use IAM roles over access keys
- Enforce MFA for all privileged accounts
- Principle of least privilege (PoLP)

#### b. Logging and Monitoring
- Enable:
  - AWS CloudTrail
  - AWS Config
  - GuardDuty
- Set up alerts on critical changes (e.g., SG rule modified)

#### c. Network Security
- Use VPC, private subnets, and bastion hosts
- Apply Security Groups and NACLs
- Limit public IP exposure

#### d. Encryption
- Encrypt data at rest with KMS
- Encrypt in transit with TLS 1.2+

#### e. Backup and DR
- Schedule regular AMI snapshots
- Test restore and DR drills
