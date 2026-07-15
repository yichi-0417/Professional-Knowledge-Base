Documentation Principles
Purpose

This repository is the Master Record of architectural work.

Its purpose is to document projects exactly as they happened, preserving architectural decisions, technical reasoning, and delivery outcomes without tailoring the content for any particular audience.

Other versions (Resume, LinkedIn, Conference Talk, Interview Notes, etc.) should always be derived from this repository rather than written independently.

Core Principles
1. Truth before impression

Record what happened.

Do not optimize the story to make it appear larger, more innovative, or more strategic than it actually was.

If a project was a PoC, write PoC.

If the objective was Cloud Migration, write Cloud Migration.

Facts remain valuable without exaggeration.

2. Record, don't interpret

Describe the work.

Avoid explaining why readers should think it is important.

Project documents record architectural decisions and delivery outcomes.

Interpretation belongs in future articles, presentations, or personal philosophy.

3. Architecture starts from Business

Every project begins with the business initiative.

Architecture exists because a business objective created technical constraints that required architectural decisions.

The narrative should therefore follow:

Business Initiative → Architecture Decisions → Project Outcomes

rather than

Technology → Implementation.

4. Organize by architectural concerns

Projects should be organized around architectural concerns instead of products or technologies.

Examples include:

Deployment Platform
Database Platform
Identity Platform
Security & Governance
Network Architecture
Operating Model

AWS services, operating systems, databases, or middleware are implementation details supporting those concerns.

5. Record decisions, not activities

The repository records architectural decisions.

Implementation work is described only when it explains why a decision was made or why an architecture evolved.

Project management activities, meetings, coordination, or routine engineering work should not become the focus.

6. Describe constraints objectively

Constraints are facts.

Do not frame them as problems or frustrations.

Document:

business constraints
technical limitations
organizational boundaries
vendor capabilities
operational requirements

The architecture exists because these constraints existed.

7. Respect system boundaries

Enterprise architecture is largely the work of defining boundaries.

When documenting a project, distinguish clearly between:

Authentication
Authorization
Credential Management
Privileged Access
Managed Service Responsibilities
Customer Responsibilities
Vendor Responsibilities

Do not merge different architectural concerns simply because they involve the same technology.

8. Technology serves architecture

Do not emphasize technology names.

Technology appears only because it supports an architectural decision.

Readers should understand why a technology was selected before noticing which technology was selected.

9. Evaluate trade-offs explicitly

Architecture is the result of evaluation.

When multiple approaches existed, document why one approach was selected over another.

Evaluation may include:

operational complexity
implementation effort
maintainability
lifecycle
cost
organizational readiness
return on investment

Not implementing something can be as important as implementing it.

10. Automation has boundaries

Automation is not a goal.

Automate where automation creates sustainable operational value.

Accept manual operations when additional automation introduces disproportionate complexity or lifecycle cost.

Architectural decisions should optimize the system rather than maximize automation.

11. Use objective language

Projects should read like engineering records.

Prefer:

designed
adopted
evaluated
revised
validated
coordinated
established
translated

Avoid:

successfully
significantly
dramatically
innovative
groundbreaking
transformed
empowered

Readers should reach those conclusions themselves.

12. Let later projects prove earlier projects

Avoid claiming long-term impact inside a project itself.

If a capability established in one project enabled a later project, allow the later project to demonstrate that relationship naturally.

Projects should only record outcomes that were true at that point in time.

Standard Project Structure

Each project follows a consistent structure:

Project

Role & Responsibilities

Key Architectural Decisions

Overall Outcomes

Projects become more complex over time, but the structure remains unchanged.

Writing Philosophy

Record every project outcome as an architect—truthfully, accurately, and without unnecessary interpretation.

The repository is not a portfolio.

It is not a marketing document.

It is a long-term engineering record of architectural work.
