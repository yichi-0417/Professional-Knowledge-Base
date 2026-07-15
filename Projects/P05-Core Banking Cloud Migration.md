# P05-Core Banking Cloud Migration

**Duration**

2025 – Present

---

# Project

A major Japanese bank launched a strategic modernization program to strengthen its competitiveness in the rapidly evolving digital banking market.

Prior to this initiative, business applications across the enterprise had already been migrated to AWS. The Core Banking platform, the most business-critical system within the bank, became the final phase of the cloud migration program.

The objective was to establish a cloud platform capable of supporting the bank's long-term business roadmap while maintaining the availability and operational requirements expected of a core banking system. The target platform was designed to support real-time transaction processing and data transformation at a scale of approximately 30 million end-user accounts by 2028.

The migration covers approximately 500 servers and databases across four environments (Development, Staging, Production, and Disaster Recovery) and nine operational domains. The design phase alone represented an investment of approximately JPY 250 million.

---

# Role & Responsibilities

## Lead Cloud Architect

Led the AWS platform architecture throughout the design and implementation phases of the Core Banking migration.

Owned architectural design and technical decision-making across deployment automation, database platforms, operating systems, identity, networking, security, governance, disaster recovery, and platform operations.

Reviewed architecture proposed by internal engineering teams and coordinated technical discussions with the customer's infrastructure department, IBM development teams, AWS Japan Professional Services, AWS Global engineering teams, Red Hat consulting team, PwC consulting team, internal Security teams, and the company's Global Headquarters throughout the project.

Led migration strategy discussions with the customer while translating operational requirements into implementable architecture across multiple engineering organizations.

---

# Key Architectural Decisions

## Enterprise Deployment Automation

The customer decided to introduce CI/CD as the standard deployment model for the Core Banking platform in order to support long-term operation of a system of this scale.

The original architecture planned to use AWS CodeCommit together with AWS CodeBuild and AWS CodePipeline. During the design phase, changes to AWS service availability made the original approach incompatible with project requirements. At the same time, customer policies required source code to remain within Japan, while deployment architecture also had to preserve strict isolation between Development, Staging, Production, and Disaster Recovery environments.

The deployment architecture was redesigned using self-managed GitLab together with AWS CodeBuild and AWS CodePipeline. GitLab servers were deployed in both Tokyo and Osaka for high availability, while deployment pipelines were separated across Tokyo and Seoul. Environment isolation was achieved through VPC Peering and subnet-level routing control rather than Transit Gateway in order to align with the customer's existing network architecture and operational policies.

---

## Amazon RDS for Db2

Following the customer's principle of adopting managed AWS services wherever practical, Amazon RDS for Db2 was selected as the database platform.

Implementation identified multiple differences between Amazon RDS for Db2, traditional Db2 environments, and operational requirements for the Core Banking platform. Backup design required both Amazon RDS snapshots and command-based database backups to satisfy recovery requirements. Database encryption introduced additional responsibility boundaries between Amazon RDS and customer-managed components. 

During implementation, IBM announced a new major version of the Db2 database engine. As Amazon RDS for Db2 follows the IBM Db2 engine lifecycle, the project was required to evaluate the impact before production deployment. The new version could not be introduced through an in-place upgrade and instead required complete instance reconstruction after infrastructure deployment had already been completed for two of the four project environments.

AWS Professional Services provided a reference solution for automating the migration using AWS Systems Manager Run Command, AWS Lambda, and AWS Step Functions. Although technically feasible, the proposed architecture introduced additional operational components whose implementation and long-term maintenance costs outweighed the expected benefits for a one-time migration. The approach also received limited support from the database engineering team because it increased operational complexity without reducing post-migration manual activities.

The migration strategy was therefore revised to automate infrastructure provisioning through CI/CD and Ansible wherever supported by the service, while database-specific configuration, user profiles, and several operational settings remained manual due to service limitations. The revised approach balanced automation with operational maintainability and required implementation schedules to be reorganized across environments while downstream middleware and database teams adjusted their deployment plans.

---

## Enterprise Identity Platform

The Core Banking platform was required to comply with the customer's enterprise identity architecture while supporting database authentication, privileged operations, and deployment automation.

Enterprise workforce identities followed the customer's existing Microsoft Active Directory and AWS identity architecture. Rather than introducing a separate authentication model, the project adopted the existing enterprise standards for account and permission management.

Database authentication introduced additional complexity through Kerberos integration between Amazon RDS for Db2 and Microsoft Active Directory. Authentication design therefore required consideration of both workforce authentication and database authentication, while maintaining compatibility with the customer's enterprise identity platform.

Deployment automation required controlled retrieval of credentials during script execution. AWS Secrets Manager was selected because it supported secure integration with AWS services while allowing deployment workflows to export credentials when required. Production privileged accounts continued to be managed through the customer's existing Privileged Access Management platform.

Authorization design also required coordination between Amazon RDS service roles, EC2 instance profiles, AWS KMS policies, and Microsoft Active Directory permissions. Although Microsoft Active Directory participated in the required permission model defined by AWS, database authentication itself remained a Kerberos trust relationship between Amazon RDS for Db2 and Microsoft Active Directory. Responsibility boundaries between authentication, authorization, credential management, and privileged access management were therefore defined explicitly before implementation.

---

## Responding to Red Hat Lifecycle Changes

During implementation, Red Hat announced changes to both product lifecycle and licensing policy.

Although the operating system could have been upgraded after production release, delaying the migration would have introduced additional operational risk to a business-critical banking system. The revised licensing model also required migration from AWS License Included subscriptions to customer-managed Red Hat subscriptions through AWS Marketplace, affecting infrastructure provisioning, repository management, and operating system maintenance design within the customer's isolated network environment.

The migration strategy was revised to complete the operating system transition before service launch. Infrastructure provisioning was automated wherever possible, while storage migration and compatibility validation were performed separately. Architecture reviews focused on migration strategy, licensing impact, schedule adjustments, and operating system maintenance architecture. After technical and commercial discussions, the customer approved the revised approach, and compatibility validation across middleware, operating systems, and application components is currently in progress.

---

## Security and Governance Baseline

At the beginning of the project, the customer's infrastructure organization planned to use the Core Banking platform as the pilot implementation for a future enterprise-wide security and governance model.

The original architecture adopted AWS Security Hub together with Amazon CloudWatch, AWS CloudTrail, AWS Config, and Datadog as the operational baseline. During implementation, the customer's Security organization introduced a different enterprise governance platform intended to provide unified compliance management across both AWS and non-AWS environments.

Although the alternative platform satisfied enterprise compliance requirements, differences in operational capabilities required the architecture to be re-evaluated from both governance and operational perspectives. At the same time, implementation scope was constrained by project budget and contractual boundaries, requiring additional discussions between architecture, security, and commercial stakeholders. The architecture continues to evolve as governance responsibilities and implementation scope are refined.

---

# Outcomes

The project remains in delivery.

Architectural decisions established during the design phase continue to guide implementation across the Core Banking migration platform.

Knowledge accumulated through Amazon RDS for Db2 implementation has become the primary internal reference for similar projects within the company's Technology Center of Excellence, and the experience gained from the project has also been applied to subsequent enterprise cloud migration programs.
