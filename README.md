# Cloud-Engineering-fundamental-Capstone-lab
 Cloud-Engineering-fundamental-Capstone-lab

  Project Overview

This project documents the design and modeling of a cloud-native AWS architecture using DiagramGPT and draw.io XML generation.

The goal is to define a structured, production-ready AWS architecture while answering key architectural decision questions such as:

Environment strategy (Production, Staging, Development)

AWS region selection

Compliance considerations

Cloud-native vs. hybrid integration

Additional AWS services and external integrations

     Architecture Scope
1.  Environments Represented

The architecture includes:

Production – Main live environment

Staging – Pre-production testing and validation

Development – Developer testing and feature implementation

Each environment is logically isolated to support secure CI/CD workflows and risk-free deployments.

2️. AWS Region & Compliance Considerations

The architecture design considers:

Region selection based on:

Latency

Cost

Regulatory requirements

Compliance requirements such as:

Data protection standards

Regional data residency policies

Industry-specific regulations (if applicable)

The design supports region-aware deployments and can be extended for multi-region high availability.

3️. Cloud-Native Strategy

The system is designed as:

- Fully Cloud-Native

There is no on-premises integration included in the current architecture. All components are designed to run entirely within AWS.

However, the architecture can be extended in the future to include:

VPN connections

AWS Direct Connect

Hybrid database replication

4️. Additional AWS Services Considered

The architecture optionally supports integration with:

IAM – Identity and access control

CloudWatch – Monitoring and logging

AWS WAF – Web application firewall

CloudTrail – Audit logging

S3 – Static assets and storage

RDS or DynamoDB – Data persistence

Elastic Load Balancer (ELB) – Traffic distribution

Auto Scaling Groups – High availability

VPC with Public/Private Subnets – Network isolation

External integrations (optional):

Third-party authentication providers

Payment gateways

Monitoring tools

🛠 Tools Used

DiagramGPT – For structured architecture generation

draw.io XML – For diagram export and visualization

Markdown – For documentation
/architecture
    ├── aws-architecture.drawio.xml
    ├── architecture-diagram.png
    

/README.md