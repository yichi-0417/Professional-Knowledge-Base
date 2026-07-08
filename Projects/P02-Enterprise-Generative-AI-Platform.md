# P02 - Enterprise Generative AI Platform

**Duration**

June 2024 – December 2024

---

## Project

Enterprise Generative AI proof-of-concept for a major Japanese credit card company within one of Japan's largest global business groups.

The project aimed to improve contact center efficiency and customer satisfaction by assisting operators during customer calls. The solution analyzed customer conversations, recommended relevant internal documentation and previous responses, and helped operators provide faster and more consistent answers.

The proof of concept was first validated through internal testing before being prepared for rollout to branch offices and partner agencies after successful evaluation.

The delivery team consisted of approximately nine members, including a Project Manager, Consulting Partner, Solution Architect, and Cloud Engineers.

---

## Role & Responsibilities

### AI Solution Architect

Owned the end-to-end cloud architecture for the enterprise Generative AI platform.

Defined architecture across compute, foundation models, retrieval, storage, networking, development environments, security, and operational design.

Reviewed all AWS architecture before customer delivery and drove technical decision-making throughout proposal refinement, architecture design, implementation, and technical validation.

Translated business requirements into executable cloud architecture while balancing delivery schedule, operational sustainability, infrastructure cost, and future extensibility.

---

### Technical Lead

Defined technical standards for the delivery team and reviewed implementation approaches throughout the project.

Provided technical guidance on Generative AI fundamentals, Retrieval-Augmented Generation (RAG), AWS architecture, and solution design.

---

## Key Decisions & Outcomes

### Designing for Technology Evolution

The initial proposal adopted Amazon Bedrock with Claude Sonnet as the primary foundation model.

During delivery, the customer requested the ability to customize part of the solution using an open-source retrieval architecture. Instead of replacing the existing design, the platform was restructured so that managed foundation models and self-managed retrieval components could evolve independently behind a common application layer.

The same architectural approach later absorbed additional technology changes, including the retirement of the managed development environment, which was replaced with a self-managed environment running on Amazon EC2 without requiring architectural redesign.

---

### Balancing AI Capability with Enterprise Delivery

The inference platform was implemented on Amazon ECS running on Amazon EC2 GPU instances to retain control over CUDA and future model customization.

During architecture design, CUDA compatibility with the latest Amazon Linux release became a delivery constraint. Rather than selecting an operating system that would require major upgrades during delivery, the architecture was revised to Red Hat Enterprise Linux while the development environment was still at an early stage, minimizing migration cost and reducing long-term operational risk.

Development environments operated entirely on CPU instances, with GPU instances introduced only after benchmark validation, allowing infrastructure cost to remain low throughout development while preserving production performance.

---

### Designing for Operational Flexibility

The original proposal adopted a managed retrieval architecture based on Amazon OpenSearch Service and Apache Cassandra.

Following customer feedback on operational flexibility, editability, and cost, the retrieval layer was redesigned using Amazon S3 together with Meta FAISS, allowing vector management to remain under application control while simplifying future customization.

The proof of concept successfully completed technical validation and was approved for rollout beyond the initial internal evaluation environment, leading to a follow-on development contract.

---

## Recognition

Received the company's quarterly **Customer Success Award** as the Solution Architect for the project following nomination by the responsible Vice President.

Presented the project as an internal case study within the Cloud organization and delivered a technical knowledge-sharing session for approximately 30 engineers in the India delivery organization. <br>

The architecture, proposal refinements, and implementation experience became reusable assets for subsequent enterprise AI proposals and delivery.
