---
date: 2025-03-18
draft: false
title: 'Principles of Good Data Architecture'
toc: true
---

# Good Data Architecture

> Data architecture is the design of systems to support the evolving data needs of an enterprise, achieved by flexible and reversible decisions reached through a careful evaluation of trade-offs.

While data engineers play a separate role from data architects, it is beneficial to have an understanding of what entails good architecture; sometimes there is an overlap in these roles, especially in organizations with low levels of data maturity.

## Principles of Good Data Architecture
Drawing from the [Principles of Good Software Architecture](Principles%20of%20Good%20Software%20Architecture.md), the principles of good data architecture are:

1. Choose common components wisely
2. Plan for failure
3. Architect for scalability
4. Architecture is leadership
5. Always be architecting
6. Build loosely coupled systems
7. Make reversible decisions
8. Prioritize security
9. Embrace FinOps

### Principle 1. Choose Common Components Wisely
Common components can be anything that has broad applicability across an organization. They should enable agility within and across teams in conjunction with shared knowledge and skills. When architects lead effectively, these common components become a fabric facilitating team collaboration and breaking down silos.

Choosing common components is a balancing act; it needs to facilitate inter-operation and collaboration, while at the same time avoid hampering engineers working on domain-specific problems. **That is, common components should serve a purpose well and enable collaboration, while avoiding lock-in.**

### Principle 2. Plan for Failure

> Everything fails, all the time.
> - Werner Vogels

To build highly robust systems, you must consider failures in your designs. The is achieved by defining and evaluating the following criteria:

1. **Availability**: the percentage of time a service or component is in a *operational state*
2. **Reliability**: the system's probability of meeting defined standards in performing its intended task within a specific time period
3. **Recovery Time Objective**: the maximum acceptable time for a service or system outage. This is usually defined based on the business impact of an outage (e.g., cost)
4. **Recovery Point Objective**: the acceptable state after recovery from an outage. In data systems, data is often lost during an outage; in this setting the recovery point objective refers to the maximum acceptable data loss

Defining acceptable criteria for the above will guide engineers in their architecture decisions as they assess possible failure scenarios.

### Principle 3. Architect for Scalability
Scalability optimizes a system to meet performance requirements based on its load, while minimizing costs. A system should be *elastic*, i.e. able to scale down when load is low to save on costs, and able to scale up when load is high to meet performance requirements.

### Principle 4. Architecture is Leadership

> The most important activity of a software architect is to mentor the development team, to raise their level so they can take on more complex issues. Improving the development team’s ability gives an architect much greater leverage than being the sole decision-maker and thus running the risk of being an architectural bottleneck.

Software architects should be highly technically competent but delegate most individual contributor work to others. They should **not** adopt a command-and-control approach, but rather be a mentor to engineers. They should make careful technology choices in consultation with their organization, and disseminate expertise through training and leadership.

### Principle 5. Always Be Architecting
An architect’s job is to develop deep knowledge of the baseline architecture (current state), develop a target architecture, and map out a sequencing plan to determine priorities and the order of architecture changes. This target architecture changes over time; it is a *moving target* adjusted to business and technology changes internally and worldwide. The sequencing plan determines *immediate priorities* for delivery.

### Principle 6. Build Loosely Coupled Systems

> When the architecture of the system is designed to enable teams to test, deploy, and change systems without dependencies on other teams, teams require little communication to get work done. In other words, both the architecture and the teams are loosely coupled.
> - Google DevOps Tech [Architecture Guide](https://cloud.google.com/architecture/devops)

The goal of building loosely coupled systems is to enable agility across development teams. This is essentially a method to reduce the dependencies of a service or component. 

For software architecture, a loosely coupled system has the following properties:

1. Systems are broken into many small components.
2. These systems interface with other services through abstraction layers, such as a messaging bus or an API. These abstraction layers hide and protect internal details of the service, such as a database backend or internal classes and method calls.
3. As a consequence of property 2, internal changes to a system component don’t require changes in other parts. Details of code updates are hidden behind stable APIs. Each piece can evolve and improve separately.
4. As a consequence of property 3, there is no waterfall, global release cycle for the whole system. Instead, each component is updated separately as changes are introduced.

Building loosely coupled systems generally helps especially when working across large numbers of teams. That isn't to say that is is not beneficial when teams are small, as loosely coupled systems tend to enable reversible decisions to be made.

### Principle 7. Make Reversible Decisions
Reversible decisions refers to changes which can be rolled back. This is especially useful when an organization needs to pivot, or if a choice seems to have not had the expected outcome.

The software landscape is changing rapidly. Today’s hot technology or stack is tomorrow’s afterthought. Popular opinion shifts quickly. You should aim for reversible decisions, as these tend to simplify your architecture and keep it agile.

### Principle 8. Prioritize Security

> Those who handle data must assume that they are ultimately responsible for securing it.

All software engineers should consider themselves security engineers, lest the organization experiences a data leak due to a lack of security. There are legal considerations to be made here as well, such as with regulations like the GDPR and CCPA.

There are two main security models to consider: zero-trust security and the shared responsibility security model.

#### Zero-Trust Security
Traditional architectures place a lot of faith in perimeter security, crudely a hardened network perimeter with “trusted things” inside and “untrusted things” outside. Unfortunately, this approach has always been vulnerable to insider attacks, as well as external threats such as spear phishing.

Zero-trust means to trust nothing, people nor machine, and always assume a security risk is present. To enforce zero-trust security within an organization, follow the [Principle of Least Privilege](Principle%20of%20Least%20Privilege.md), and implement access restrictions via methods like IAM.

#### The Shared Responsibility Security Model 
This security model is most popular within cloud environments, and divides security into the security *of* the cloud and the security *in* the cloud.

In general, all cloud providers operate on this shared responsibility model. They secure their services according to published specifications, while leaving it up to the user to design a security model for their applications and data. 

### Principle 9. Embrace [FinOps](FinOps.md)
As a cost-optimization technique focused on driving revenue, FinOps is invaluable in delivering value for your organization.

# Recommended Reading
It is suggested to review the [Major Software Architecture Concepts](Major%20Software%20Architecture%20Concepts.md), to gain an understanding of some critical concepts in software architecture like distributed systems and monoliths, as well as brownfield and greenfield projects.
