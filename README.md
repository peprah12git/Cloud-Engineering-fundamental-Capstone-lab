<h1 align="center"> AWS Multi-Tier Architecture Blueprint ☁️</h1>

## Project Overview

This project evaluates a two-tier on-premises web application and proposes a modern cloud-native AWS architecture. It follows AWS best practices using the **Well-Architected Framework (WAF)** and **Cloud Adoption Framework (CAF)**.

---

##  1. Existing Architecture

- **Frontend:** Single web server (Apache/Nginx, Node.js/PHP/Java) handling requests and business logic
- **Backend:** Relational database (MySQL/PostgreSQL) with local storage, no redundancy
- **Networking:** Single network, public IP, basic firewall

**Risks:**
- Single point of failure
- No monitoring
- Security vulnerabilities
- Data loss risk
- Limited scalability
- High operational overhead

---

##  2. Well-Architected Evaluation

| Pillar        | Strength                | Improvement                        | AWS Services                        |
|-------------- |------------------------|------------------------------------|-------------------------------------|
| Operational   | Simple architecture    | Automate monitoring & deployments  | CloudWatch, CloudTrail, CodePipeline|
| Security      | Basic firewall         | Enforce least privilege, WAF       | IAM, Security Groups, WAF           |
| Reliability   | Logical tier separation| Multi-AZ, backups                  | RDS Multi-AZ, Auto Scaling, ELB     |
| Performance   | Handles low traffic    | Dynamic scaling                    | Auto Scaling, CloudFront            |
| Cost          | No cloud costs         | Elastic resources, right-sizing     | Cost Explorer, EC2, RDS             |

---

##  3. CAF Readiness

- **Business:** Define cloud objectives, KPIs, and ROI
- **People:** Train teams on AWS and DevOps, establish CCoE
- **Governance:** Enforce policies, IAM, budgets, and compliance
- **Platform:** VPC with public/private subnets, Multi-AZ, IaC, managed services
- **Security:** IAM least privilege, MFA, encryption, WAF, centralized logging
- **Operations:** CloudWatch monitoring, CI/CD, automated backups, runbooks

---

##  4. Improved Architecture

### Cloud-Native Design

- **Networking:** VPC with public/private subnets across multiple AZs
- **Compute:** EC2 Auto Scaling behind ALB
- **Database:** Amazon RDS Multi-AZ with backups
- **Security:** IAM, WAF, Security Groups, TLS & encryption
- **Monitoring:** CloudWatch & CloudTrail
- **DevOps:** CI/CD pipelines via CodePipeline, Infrastructure as Code


---

## 🎯 Key Outcomes

- High availability and scalability
- Enhanced security and monitoring
- Reduced operational burden
- Predictable cost and automated deployments

---

## 🛠️ AWS Services Used

EC2, RDS, ALB, Auto Scaling, VPC, IAM, WAF, CloudWatch, CloudTrail, CodePipeline, CloudFormation/Terraform

Networking: VPC with public/private subnets across multiple AZs

Compute: EC2 Auto Scaling behind ALB

Database: Amazon RDS Multi-AZ with backups

Security: IAM, WAF, Security Groups, TLS & encryption

Monitoring: CloudWatch & CloudTrail

DevOps: CI/CD pipelines via CodePipeline, Infrastructure as Code

Diagram Concept:

Users → Route 53 → ALB → Auto Scaling EC2 → RDS Multi-AZ
Key Outcomes

High availability and scalability

Enhanced security and monitoring

Reduced operational burden

Predictable cost and automated deployments

AWS Services Used

EC2, RDS, ALB, Auto Scaling, VPC, IAM, WAF, CloudWatch, CloudTrail, CodePipeline, CloudFormation/Terraform
