Task 1 – Review of the Existing Architecture
Overview

The organization is migrating a two-tier web application from on-premises infrastructure to AWS. The current setup consists of a frontend web server and a backend relational database hosted within a single on-premises environment.

This review consolidates all identified components, risks, and weaknesses into one clear and structured assessment aligned with AWS best practices.

Components of the Workload
Frontend Tier (Web/Application Layer): consists of a web application hosted on a single on-premises server. This server handles user requests, processes business logic, and serves both static and dynamic content. The application is likely exposed through a public IP address, making it accessible over the internet. It typically runs on web servers such as Apache or Nginx, with backend logic implemented using technologies like Node.js, PHP, or Java, and static files stored locally on the same machine.

Backend Tier (Database Layer): consists of a relational database server, such as MySQL or PostgreSQL, hosted on an on-premises machine, either on a separate server or possibly on the same physical system as the web application. This database is responsible for storing critical application data, including user information, transactions, and system logs. The data is stored on local disk storage, with no external replication, redundancy, or high-availability mechanism in place, increasing the risk of data loss in the event of hardware failure.

Networking: Single network, public IP, basic firewall rules.

Potential Risks or weakness
1. Single Point of Failure: Both the web server and database server are hosted on single machines, creating a single point of failure. If either server experiences hardware failure, software issues, or security breaches, the entire application will become unavailable.
2. Scalability Issues: The current architecture does not support horizontal scaling. As user demand increases, the web server and database may become overwhelmed, leading to performance degradation and potential downtime.
3. he system lacks monitoring and logging capabilities, with no centralized logging, automated alerts, or performance tracking in place, making it difficult to detect failures, identify security incidents, or analyze system performance issues in a timely manner.
4. Security Vulnerabilities: The application is exposed to the internet without proper security measures such as firewalls, intrusion detection systems, or regular security updates, increasing the risk of cyberattacks and data breaches.
5. Data Loss Risk: The database lacks redundancy and backup mechanisms, making it vulnerable to data loss in the event of hardware failure, software corruption, or cyberattacks.
6. Maintenance Challenges: The on-premises setup requires manual maintenance, including hardware upkeep, software updates, and security patches, which can be time-consuming and prone to human error.

These are the some of the reasons for Aws best practice when business want to migrate from On-premise to cloud.


Task 2 – Evaluate the Workload Using the AWS Well-Architected Framework
Below is a clear and structured evaluation of the existing two-tier workload using the five AWS Well-Architected pillars, identifying one strength, one area for improvement, and a recommended AWS service for each pillar.

| Pillar                | Observation (Strength)                                                                 | Improvement Recommendation                                                                                  | Supporting AWS Service                                 |
|-----------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|
| Operational Excellence| The system architecture is simple and easy to understand due to its two-tier structure.| Implement automated monitoring, logging, and deployment processes to reduce manual operations and improve visibility.| Amazon CloudWatch, AWS CloudTrail, AWS CodePipeline   |
| Security              | Basic firewall rules are in place to restrict some access.                             | Enforce least-privilege access, secure networking, and protect against external threats using layered security controls.| AWS IAM, Security Groups, AWS WAF                     |
| Reliability           | Separate frontend and backend tiers provide logical separation of responsibilities.     | Eliminate single points of failure by enabling Multi-AZ deployments and automated backups.                  | Amazon RDS Multi-AZ, EC2 Auto Scaling, Elastic Load Balancer |
| Performance Efficiency| Current setup may handle predictable, low traffic workloads adequately.                | Enable dynamic scaling and performance monitoring to handle traffic spikes efficiently.                     | EC2 Auto Scaling, Amazon CloudFront                    |
| Cost Optimization     | On-prem infrastructure may already be fully owned (no ongoing cloud compute cost yet). | Use right-sizing, elastic resources, and managed services to avoid over-provisioning in AWS.                | AWS Cost Explorer, EC2 Auto Scaling, Amazon RDS        |

Task 3.Task 3 – Apply the AWS Cloud Adoption Framework (CAF)

Below is an analysis of the organization’s readiness using the six AWS CAF perspectives, including key actions needed for successful migration.

1. Business Perspective 
From a business perspective, the organization is motivated to migrate in order to improve scalability, availability, and long-term cost efficiency. However, current operations rely on traditional on-premises infrastructure, which may indicate limited financial modeling for cloud consumption-based pricing. The organization appears technically driven but may lack a clearly defined cloud business case, including ROI projections, cost forecasting, and defined success metrics such as improved uptime or faster deployment cycles.

To ensure readiness, leadership must define clear migration objectives aligned with business outcomes. Key actions include developing a cloud financial model, identifying measurable KPIs (availability targets, recovery time objectives, performance benchmarks), and creating a phased migration roadmap. Stakeholder alignment is also critical to ensure technical teams and business leaders share common expectations. Establishing executive sponsorship and defining cloud value propositions will help ensure long-term sustainability and strategic alignment with growth objectives.

2. People Perspective 
The organization likely has experience managing traditional servers but may have limited hands-on expertise with AWS services, DevOps practices, and infrastructure automation. This skills gap represents a readiness challenge, particularly in areas such as IAM, networking, monitoring, and cost optimization in the cloud environment.

To enable successful migration, investment in training and certification is essential. Team members should pursue AWS foundational and associate-level certifications to build competency in architecture, security, and operations. Introducing a Cloud Center of Excellence (CCoE) can help guide best practices and governance standards. Additionally, adopting DevOps culture—encouraging collaboration between development and operations teams—will improve automation and deployment reliability. Clear role definitions for cloud architects, security engineers, and operations staff will further enhance accountability and reduce transition risks

3. Governance Perspective (≈170 words)
Currently, governance processes appear informal, with manual operations and limited oversight of security configurations, backups, and monitoring. This indicates low cloud governance maturity. Migrating without proper guardrails could result in uncontrolled costs, inconsistent configurations, or security vulnerabilities.

To strengthen governance readiness, the organization should implement policy frameworks before migration. Key actions include defining cloud usage policies, enforcing tagging standards for cost tracking, and establishing account structures using AWS Organizations. Role-based access control through IAM policies should be strictly enforced under the principle of least privilege. Financial governance mechanisms such as budgets and cost alerts must also be configured to prevent overspending. Additionally, compliance requirements (data protection, logging retention policies, and audit trails) should be clearly documented and automated where possible. Strong governance ensures consistency, accountability, and risk management throughout the cloud lifecycle.

4. Platform Perspective (≈180 words)

The current platform is a simple two-tier on-prem architecture with limited scalability and redundancy. This indicates low cloud platform maturity, particularly in high availability, elasticity, and automation capabilities. However, the application’s simplicity makes it a good candidate for migration using a phased or re-architect approach.

Key enablers include designing a Virtual Private Cloud (VPC) with public and private subnets across multiple Availability Zones. Compute resources should be deployed using Auto Scaling groups behind an Elastic Load Balancer. The database should be migrated to Amazon RDS with Multi-AZ enabled for high availability. Infrastructure as Code (IaC), using AWS CloudFormation or Terraform, should be adopted to ensure repeatable and consistent deployments. Incorporating managed services rather than self-managed EC2 instances will reduce operational burden and improve resilience. This platform modernization will align the workload with AWS best practices for reliability and scalability.

5. Security Perspective 

Security posture in the current environment appears basic, with simple firewall rules and public exposure risks. There is limited visibility, no centralized logging, and no evidence of layered defense mechanisms. This presents a significant cloud readiness gap.

Before migration, a security baseline must be established. Key actions include implementing IAM with least-privilege policies, enabling multi-factor authentication (MFA), and designing secure VPC segmentation (public subnets for web tier, private subnets for database tier). Encryption should be enforced both in transit (TLS certificates via AWS Certificate Manager) and at rest (RDS encryption, EBS encryption). AWS WAF and security groups should be configured to restrict traffic appropriately. Centralized logging using CloudTrail and CloudWatch should be enabled to support auditing and incident response. Proactively embedding security controls ensures that migration does not replicate on-prem weaknesses in the cloud.

6. Security Perspective 
Security posture in the current environment appears basic, with simple firewall rules and public exposure risks. There is limited visibility, no centralized logging, and no evidence of layered defense mechanisms. This presents a significant cloud readiness gap.

Before migration, a security baseline must be established. Key actions include implementing IAM with least-privilege policies, enabling multi-factor authentication (MFA), and designing secure VPC segmentation (public subnets for web tier, private subnets for database tier). Encryption should be enforced both in transit (TLS certificates via AWS Certificate Manager) and at rest (RDS encryption, EBS encryption). AWS WAF and security groups should be configured to restrict traffic appropriately. Centralized logging using CloudTrail and CloudWatch should be enabled to support auditing and incident response. Proactively embedding security controls ensures that migration does not replicate on-prem weaknesses in the cloud.

7. Operations Perspective 
Operationally, the organization relies heavily on manual processes, including deployments, scaling, and troubleshooting. There is limited automation, no centralized monitoring, and no formal incident response procedures. This indicates low operational readiness for cloud environments, which require continuous monitoring and automation-driven management.

To improve readiness, operational processes must be modernized. Implementing Amazon CloudWatch for monitoring and alerting will provide visibility into system health and performance. Automated backup policies and disaster recovery planning should be defined, including Recovery Time Objectives (RTO) and Recovery Point Objectives (RPO). CI/CD pipelines using AWS CodePipeline or similar tools should be introduced to automate application deployments. Infrastructure as Code will further reduce manual errors and configuration drift. Finally, documenting operational runbooks and incident response procedures will enhance resilience and ensure faster recovery from failures.

Task 4: Design an Improved Architecture
