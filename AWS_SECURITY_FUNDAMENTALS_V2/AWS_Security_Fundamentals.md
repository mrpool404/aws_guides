# # AWS Security Fundamentals
### # Table of Contents

- [Introduction]()
- [AWS Global Infrastrcutre]()
- [Data Center Security]()
- [Compliance and Governance]()
- [Entry Points in AWS]()
- [Identity & Access Management (IAM)]()
- [Detective Controls]()
- [Infrastrcture Protection]()
- [Data Protection]()
- [Incident Response]()
- [DDoS Mitigation]()
- [AWS Well-Architectured Tool]()

---

### # Introduction

- Cloud Security Design Principles:
    - **Implement a stron identity foundation** 
    - **Enable traceability**
    - **Apply security at all layers**
    - **Automate security best practices**
    - **Protect data in transit and at rest**
    - **Enforce the principle of least privilege**
    - **Preapare for security events**
- AWS shared responsibility model states that AWS is responsible for protecting the globlal infrastructure that runs all the services provided by AWS (security of the cloud) while the customer is responsible for protecting their data, os, networks and other resources that are created in the AWS (security in the cloud)

---

### # AWS Global Infrastrcture

- Physical data centers are grouped into logical units called 'Availability Zones'
- These availability zones are connected using low latency connections and can be considered as one large data center
- Availability zones are connected to form 'Region'

---

### # Data Center Security

- Customers can't visit AWS data centers to verfiy the security however AWS conducts Audits with external certifying authorities to validate it's security and compliance standards
- **Permitere Layer**: Data Centers are in undisclosed location under constant surveilance with access provided to personnels for only the specified amount of time that is required to carry out their responsibilites
- **Environment Layer**: AWS locates it's data centers to reduce disaster impact and reduces it's effect on environmental effect
- **Infrastrcture Layer**: The servers are protected with power backup solutions, fire suppressions mechanisms, HVAC systems,etc.
- **Data Layer**: Even though data protection is customer responsibility, AWS protects data by decomissioning storage devices using NIST800-88 techniques

---

### # Compliance and Governance

- AWS provides insights to it's security and control mechanisms through industry recognised certifications and providing reports and other documentations under NDA
- **AWS Artifact** is no cost self service portal to obtain AWS security and compliance reports

---

### # Identity and Access Mangement

- All the requests made to AWS are authenticated using IAM irrespective of their origin
- IAM is a centralized mechanism for creating and managing individual users and their permissions with your AWS account
- There are IAM Users and IAM Groups which are collection of Users
- Types of AWS Credentials:
    - Username & Password: Generally humans with passwords which follow a specific password policy to create strong passwords
    - Multifactor authentication: Additional layer of security to Passwords which can he physical or virtual
    - User Access Key: Used to make programmatic calls to AWS which consist of Access Key ID and secrete key
    - Amazon EC2 Key Pairs: A public and private key pair to access EC2 instances. However they do not provide accountability and hence it is recommended to use AD or LDAP authentication for frequent use
- Additional AWS services that facilitate IAM:
    - AWS Secrets Manager: Used to manage secrets and credentials
    - AWS Single Sign On (SSO): allows central management of SSO and access using corporate credentials
    - AWS Simple Token Service (STS: web service that enbles one to request temporary token to assume a different role to perform a specific task that is not usually performed by the entity
    - AWS Directory Service: Managed Microsoft AD is a cloud based AD for your workloads
    - AWS Organisation: manage multiple aws accounts
    - AWS Cognito: lets you sign up , sign in and manage users to your web apps and services directly using AWS cognito or through third party idenity providers

---

### # Detective Controls

- AWS CloudTrail detects and logs api calls made to your account
- It logs user identity, locations of the reuqest initiation, time, effect, etc.
- AWS CloudWatch is used to route the logs to monitor the resources, send notification and take actions based on rules
- CloudWatch evenets which are stream of system events in AWS (creation of a resource, deletion of resource, editing a resource, etc.) and CloudWatch alarms (an anomaly in current state of resources can raise an alarm) can trigger the alerting or response mechanism using AWS Simple Notification Service (SNS) or AWS Lambda
- AWS Management Console along with AWS CLI can produce powerfull audits across multiple regulatory standards for wide range of services like:
    - AWS S3 Server Access Logs
    - Elastic Load Balance Logs
    - Amazon CloudWatch Logs and Events
    - Amazon VPC Flow Logs
    - AWS CloudTrail
- Additional services that aid in detective controls:
    - Amazon GuardDuty - a ml based service to identify attack patterns
    - AWS Trusted Advisor - advisory notifications and best practices for your aws infrastrcture with respect to costing, performance, security, etc.
    - AWS VPC Flow Logs - build in access control and audit for VPC
    - AWS Security Hub - single pane glass view of the security posture of your AWS account
    - AWS Config - continous monitoring and assesment service that helps detect non compliant configurations almost in real time

---

### # Infrastructure Protection

- **Protection via Isolation**: Amazon VPC allows you to isolate your AWS resources using the following features
    - **Subnet Routing**: enable to group instances & resources based on security and operational needs and also configure routing
    - **Network ACLs**: additional layer of security that act as a firewall to ALLOW or DENY specific traffic
    - **Security Group**: virtual statefull (outbound traffic allowed for all inbound allowed connections) firewall for your connections based on rules for source and destination
- **Application & OS security**: AWS Systems Manager includes cabailities to automate tasks such as collecting system inventory, applying os patches, maintaining up to date antivirus patches, etc.
- **AWS Firewall Manager**: allows you to centrally manage and configure AWS WAF rules across multiple accounts and applications.
- **AWS Direct Connect**: used to establish secure direct network connection to on premise network to increase security and performance
- **AWS CloudFormation**: automates task of repeatedly creating and deploying AWS resources in consisten manner. Ensures compliant resources are deployed in your AWS environment.
- **AWS Inspector**: automated security assessment service that helps improve the security and compliance of AWS environment

---

### # Data Protection

- **Protection at Rest**: AWS encrypts data on your behalf after it has been recieved by the service
- **Protection in Transit**: AWS services provides HTTPS communication with AWS API providing end-to-end encryption. AWS also enables you to generate and use SSL certifcates. Use of IPSec and VPN allows to encrypt network traffic
- **AWS CloudHSM**: provides Hardware Security Model in AWS Cloud to generate, store, import, export, and manage cryptographic keys, including symmetric keys and asymmetric key pairs
- **Amazon S3 glacier**: storage service optimized for infrequently used data, also called cold data
- **AWS Certificate Manager**: handles the complexity of creating and managing public SSL/TLS certificates for your AWS based websites and applications. ACM can also be used to issue private SSL/TLS X.509 certificates that identify users, computers, applications, services, servers, and other devices internally
- **Amazon Macie**: ML based service to automatically discover, classify, and protect sensitive data in AWS
- **AWS KMS**: managed key management service with HSM support and integration with other AWS services to meet the reulatory and compliance needs

---

### # Incident Response
- Incident Response can be easily automated in AWS using the API
- AWS API enable to quickly take routine actions and features like AWS EBS snapshots allow to capture information to perform forensics on
- AWS Cloudformation along with AWS Step functions and AWS Lambda can help in forming a forensic investigation environment with preconfigured tools and incident data
- An example workflow for incident response:
    - A compormised instance is detected using third party tool and it publishes it's id to SNS topic
    - Instance is removed from the autoscaling group, snapshot is created of attached EBS volumes, instance metadata is recorded, quarantine tag is attached and the team is notified
    - Instance is isolated by removing all the previously attached SGs and new SG is assigned with no ingress or egress
    - AWS Cloudformation is used to creat an environment to investigate the compormised resources
    - Basic forensic investigation can be automated and generated reports can be sent to the team through SNS

---
### # DDoS Mitigation
- **Protection at Edge**: AWS Edge locations are ideal for absorbing DDoS attacks. Edge locations are physical data centers located in key cities, that are different from Availability Zones. As access to certain data increases with time, this data is copied to an edge location near your customer base for better performance and latency. Threats can then be taken care of at these edge locations, away from your web applications, AWS resources, and the original data
- **AWS Services for Out-of-Region Protection**: Following services provide flexible layered security protection against DDoS attacks:
    - **Amazon Route53**: Highly available and scalable DNS service that can be used to direct traffic to your web application with features like traffic flow, latency-based routing, weighted round-robin, Geo DNS, health checks, and monitoring
    - **Amazon CloudFront**: CDN to deliver HTTP and HTTPS content across the globe
    - **AWS Shield**: Managed DDoS protection service that safeguards web applications and provides additional mitigation to avoid downtime
    - **AWS WAF**: Web Application Firewall to protect your applications against availability and security

---
### # AWS Well-Architected Tool
- It is a self-service tool that is designed to help customers review AWS workloads at any time, without the need for an AWS Solutions Architect.

---

### Next Courses Recommended : 
- [Architecting on AWS](https://www.aws.training/training/schedule?courseId=10002)
- [Security Engineering on AWS](https://www.aws.training/training/schedule?courseId=10021)

---
### # References
- [AWS Security Fundamentals (Course)](https://www.aws.training/Details/eLearning?id=34259)
- [AWS Cloud Adaption Framework Security Perspective](https://d1.awsstatic.com/whitepapers/AWS_CAF_Security_Perspective.pdf)
- [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)
- [AWS Data Centers](https://aws.amazon.com/compliance/data-center/data-centers/)
- [AWS Artifact](https://aws.amazon.com/artifact/)
- [AWS Compliance Programs](https://aws.amazon.com/compliance/programs/)
- [AWS Compliance Center](https://aws.amazon.com/financial-services/security-compliance/compliance-center/?country-compliance-center-cards.sort-by=item.additionalFields.headline&country-compliance-center-cards.sort-order=asc&awsf.country-compliance-center-master-filter=*all)
- [AWS Compliance Resources](https://aws.amazon.com/compliance/resources/)
- [AWS CIS Web Services Foundataions](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)
- [AWS IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [AWS Password Policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html)
- [Cloud Audit Academy - Cloud Agnostic (Course)](https://www.aws.training/Details/eLearning?id=41556)
- [Security at Scale: Logging in AWS](https://d1.awsstatic.com/whitepapers/compliance/AWS_Security_at_Scale_Logging_in_AWS_Whitepaper.pdf)
- [CloudWatch Events Tutorial](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/CloudWatch-Events-Tutorials.html)
- [AWS Systems Manager Features](https://aws.amazon.com/systems-manager/features/)
- [Overview of AWS Security - Network Security](https://d1.awsstatic.com/whitepapers/Security/Networking_Security_Whitepaper.pdf)
- [Securing Your EC2 Instances](https://aws.amazon.com/articles/tips-for-securing-your-ec2-instance/)
- [Amazon Inspector Assessments](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_rule-packages.html)
- [AWS Systems Manager Use Cases](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-best-practices.html)
- [Protecting Data in AWS S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/DataDurability.html)
- [AWS Encryption Videos](https://www.youtube.com/user/AmazonWebServices/search?query=encryption)
- [AWS KMS Cryptographic Details](https://d0.awsstatic.com/whitepapers/KMS-Cryptographic-Details.pdf)
- [AWS VPN Connections Details](https://docs.aws.amazon.com/vpc/latest/userguide/vpn-connections.html)
- [Building a Cloud Specific Incident Response Plan](https://aws.amazon.com/blogs/publicsector/building-a-cloud-specific-incident-response-plan/)
- [AWS Incident Response Playlist](https://www.youtube.com/user/AmazonWebServices/search?query=incident+response)
- [AWS Best Practices for DDoS Resiliency](https://d0.awsstatic.com/whitepapers/Security/DDoS_White_Paper.pdf)
- [AWS Global Edge Network](https://aws.amazon.com/cloudfront/features/?whats-new-cloudfront.sort-by=item.additionalFields.postDateTime&whats-new-cloudfront.sort-order=desc)
- [AWS Well-Architected Tool](https://console.aws.amazon.com/wellarchitected/)
- [AWS Well-Architected Tool User Guide](https://docs.aws.amazon.com/wellarchitected/latest/userguide/wellarchitected-ug.pdf)
- [AWS News Blog by Jeff Barr](https://aws.amazon.com/blogs/aws/new-aws-well-architected-tool-review-workloads-against-best-practices/)
- [AWS Well-Architected Tool Demo](https://d3nn3d4w2aqyem.cloudfront.net/mp4/Getting_started_video.mp4)