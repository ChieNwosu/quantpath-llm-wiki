# AWS Certified Cloud Practitioner — CLF-C02

**Summary**: Knowledge map for the AWS Certified Cloud Practitioner exam (CLF-C02). Organized around the four official exam content domains.
**Type**: Molecule note
**Sources**: (source: AWS Certified Cloud Practitioner Exam Guide, CLF-C02)
**Last updated**: 2025-07-10
**Visibility**: PORTFOLIO_SAFE
**Exam date**: June 17, 2026

---

## Exam Overview

The CLF-C02 is AWS's foundational certification. It validates broad understanding of the AWS Cloud, its core services, security model, pricing, and support structures. It does not require hands-on technical depth — it tests conceptual understanding and the ability to identify the right AWS service for a given scenario.

**Exam format**: 65 questions (multiple choice + multiple response), 90 minutes
**Passing score**: 700/1000
**Official guide**: [AWS CLF-C02 Exam Guide](https://aws.amazon.com/certification/certified-cloud-practitioner/)

---

## Domain 1: Cloud Concepts (24%)

Core ideas about what cloud computing is and why it matters.

### Key Topics
- Benefits of cloud computing (agility, elasticity, cost savings, global reach)
- Cloud deployment models: public, private, hybrid
- Cloud service models: IaaS, PaaS, SaaS
- AWS global infrastructure: Regions, Availability Zones, Edge Locations
- AWS Well-Architected Framework (6 pillars)

### Notes to Create / Link
- [[cloud-computing]] — what cloud computing is, IaaS/PaaS/SaaS [needs note]
- [[cloud-architecture]] — AWS global infrastructure, regions, AZs
- [[aws-well-architected-framework]] — 6 pillars [needs note]

---

## Domain 2: Security and Compliance (30%)

The largest domain. Focuses on the shared responsibility model, IAM, and compliance concepts.

### Key Topics
- Shared Responsibility Model (AWS vs. customer responsibilities)
- IAM: users, groups, roles, policies, MFA
- AWS security services: Shield, WAF, GuardDuty, Inspector, Macie
- Compliance programs and AWS Artifact
- Data protection: encryption at rest and in transit, KMS
- Principle of least privilege

### Notes to Create / Link
- [[shared-responsibility-model]] — who is responsible for what [needs note]
- [[iam]] — identity and access management
- [[aws-security-services]] — Shield, WAF, GuardDuty overview [needs note]

---

## Domain 3: Cloud Technology and Services (34%)

The largest domain by content. Covers the core AWS service categories.

### Key Topics
- **Compute**: EC2, Lambda, Elastic Beanstalk, ECS, EKS
- **Storage**: S3, EBS, EFS, S3 Glacier
- **Database**: RDS, DynamoDB, Aurora, Redshift, ElastiCache
- **Networking**: VPC, subnets, security groups, Route 53, CloudFront
- **Management & Monitoring**: CloudWatch, CloudTrail, Config, Trusted Advisor
- **Developer Tools**: CodeCommit, CodeBuild, CodeDeploy, CodePipeline
- **AI/ML**: SageMaker, Rekognition, Comprehend, Polly, Lex, Bedrock
- **Migration**: Snow family, Database Migration Service, Application Migration Service

### Notes to Create / Link
- [[lambda]] — serverless compute
- [[aws-s3]] — object storage
- [[amazon-bedrock]] — foundation models and AI services
- [[athena]] — serverless SQL on S3
- [[glue]] — ETL service
- [[ec2]] — virtual machines [needs note]
- [[rds]] — relational database service [needs note]
- [[vpc]] — virtual private cloud [needs note]
- [[cloudwatch]] — monitoring and observability [needs note]

---

## Domain 4: Billing, Pricing, and Support (12%)

Understanding how AWS charges for services and what support options exist.

### Key Topics
- AWS pricing models: On-Demand, Reserved Instances, Savings Plans, Spot Instances
- AWS Free Tier (12-month, always-free, trial)
- Total Cost of Ownership (TCO) and cost optimization
- AWS Cost Explorer, Budgets, Cost and Usage Report
- AWS support plans: Basic, Developer, Business, Enterprise On-Ramp, Enterprise
- AWS Trusted Advisor (cost, security, performance, fault tolerance, service limits)

### Notes to Create / Link
- [[aws-pricing-models]] — On-Demand vs Reserved vs Spot vs Savings Plans [needs note]
- [[aws-support-plans]] — Basic through Enterprise [needs note]
- [[aws-cost-management]] — Cost Explorer, Budgets, TCO [needs note]

---

## Study Resources

- AWS Skill Builder: CLF-C02 Official Practice Question Set (free)
- AWS Skill Builder: Cloud Practitioner Essentials course (free)
- AWS Whitepapers: Overview of Amazon Web Services, AWS Well-Architected Framework
- Stephane Maarek / Neal Davis Udemy courses (recommended by community)
- NotebookLM: ingest AWS whitepapers and exam guide for enriched study notes

---

## Related Notes

- [[aws-certifications]] — certification index and status
- [[moc-aws-cloud]] — AWS knowledge map
- [[clf-c02-june-17-study-plan]] — operational study plan
- [[cloud-architecture]]
- [[iam]]
- [[amazon-bedrock]]
- [[aws-s3]]
- [[lambda]]
- [[athena]]
- [[glue]]

---

## Concept Notes Needed for Full CLF-C02 Coverage

These notes do not yet exist in the vault and should be created as study progresses:

| Note | Domain | Priority |
|---|---|---|
| `shared-responsibility-model.md` | Security | High |
| `aws-well-architected-framework.md` | Cloud Concepts | High |
| `cloud-computing.md` | Cloud Concepts | High |
| `ec2.md` | Technology & Services | High |
| `rds.md` | Technology & Services | Medium |
| `vpc.md` | Technology & Services | Medium |
| `cloudwatch.md` | Technology & Services | Medium |
| `aws-pricing-models.md` | Billing | Medium |
| `aws-support-plans.md` | Billing | Medium |
| `aws-security-services.md` | Security | Medium |
| `aws-cost-management.md` | Billing | Low |
