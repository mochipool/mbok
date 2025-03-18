---
date: '2025-03-18T01:47:37-04:00'
draft: false
title: 'Guide to Designing Good Software Architecture'
---

This guide intends to provide a brief, yet actionable overview of good software architecture concepts for your organization. It focuses on pragmatic principles which serve to overcome many of the pitfalls in developing a software architecture. Finally, it will introduce a framework for selecting the appropriate technologies to utilize within your software architecture.

> Architecture is strategic; technology is tactical.

# Principles of Software Architecture
Good software architecture should empower developers and teams to innovate, move with agility, and deliver value quickly and reliably. It is a strategic design with the goal of enabling your organization to continuously deliver value while reducing the friction at each step.

Some of the core principles which serve as the foundation for such an architecture are as follows:

- Choose common component wisely; avoid technologies that hamper engineers and have vendor lock-in
- Plan for failure; assess recovery time objectives and recovery point objectives
- Architect for scalability; enable your services to scale up and down as needed
- Always be architecting; reassess your architecture to ensure that it meets business goals
- Build loosely coupled systems which reduce dependencies across services
- Make reversible decisions; these tend to keep your architecture agile
- Prioritize security
- Embrace FinOps

For a more in-depth explanation of each of these concepts, see the document [Good Data Architecture](../concepts/Good%20Data%20Architecture.md). It may be a good idea to also read up on [Major Software Architecture Concepts](../concepts/Major%20Software%20Architecture%20Concepts.md) as a primer on the high-level software concepts.

# Tactics of Technology Selection
With the architecture out of the way, you will need to select technologies which will help fulfill your architecture's goals. Though this may seem a trivial task given the vast array of technologies to choose from, this comes with the downside of *analysis paralysis*, as well as *shiny object syndrome*, among others.

A brief overview of the major points are as follows:

- Assess the team's capabilities for implementing and managing the technology
- What is the time to value for the technology?
- Interoperability with other technologies across your architecture
- How immutable and stable is the technology?
- Total cost of ownership; does it require capex or is it opex?
- Opportunity cost; how quickly and easily can you switch out of the technology if things go south?
- Does building a new technology solution instead of using an existing one offer a competitive advantage? Does it deliver sufficient value?

It is suggested to read the document [Software Architecture Technology Selection](../concepts/Software%20Architecture%20Technology%20Selection.md) for a complete rundown of the tactics involved in selecting appropriate technologies for your software architecture.
