# quickstart-irap-protected
## IRAP PROTECTED Reference Architecture on the AWS Cloud

**IRAP PROTECTED** meets the Australian Cyber Security Centre (ACSC) Information Security Manual (ISM) requirements for sensitive government data handling at the PROTECTED classification level.

This Quick Start reference deployment guide provides step-by-step instructions for deploying the Information Security Registered Assessors Program (IRAP) PROTECTED Reference Architecture on the AWS Cloud.

![Quick Start Architecture for IRAP PROTECTED](https://d0.awsstatic.com/partner-network/QuickStart/compliance-irap-protected-architecture.png)

The Quick Start sets up the following:
- A highly available architecture that spans three Availability Zones.
- A VPC configured with public and private subnets, according to AWS best practices, to provide you with your own virtual network on AWS.
- In the public subnets, managed network address translation (NAT) gateways to allow outbound internet access for resources in the private subnets.
- Three types of private subnets:
  - The web app subnet contains an Auto Scaling group of Linux webservers running Apache.
  - The database subnet contains an Amazon Relational Database Service (Amazon RDS) instance running MySQL that is configured for multiple Availability Zones.
  - The Lambda subnet contains a Lambda function that synchronizes the Network Load Balancer (NLB) target group to the Application Load Balancer (ALB). This pattern is only required if the customer wants to make the application available to other AWS-based environments through [AWS PrivateLink](https://aws.amazon.com/privatelink/).
- Amazon CloudWatch for monitoring the webservers and Lambda functions.
- AWS Identity and Access Management (IAM) for managing access to resources.
- AWS Key Management Service (AWS KMS) for encryption.
- AWS Web Application Firewall (AWS WAF) for layer 7 protections.
- Amazon GuardDuty to perform continuous monitoring for malicious activity and unauthorized behavior.

This Quick Start assumes familiarity with the IRAP PROTECTED Reference Architecture. For more information, see [AWS Artifact](https://aws.amazon.com/artifact/) and [IRAP compliance](https://aws.amazon.com/compliance/irap/).

For architectural details, best practices, step-by-step instructions, and customization options, see the [deployment guide](https://fwd.aws/D9yDG). This guide requires a moderate level of familiarity with AWS services. If you’re new to AWS, visit the [Getting Started Resource Center](https://aws.amazon.com/getting-started/) and the [AWS Training and Certification](https://aws.amazon.com/training/) website for materials and programs that can help you develop the skills to design, deploy, and operate your infrastructure and applications on the AWS Cloud.

To post feedback, submit feature ideas, or report bugs, use the **Issues** section of this GitHub repo.
If you'd like to submit code for this Quick Start, please review the [AWS Quick Start Contributor's Kit](https://aws-quickstart.github.io/).
