---
date: 2025-03-18
draft: false
title: 'Major Software Architecture Concepts'
toc: true
---
This document presents an overview of some of the major architectural concepts in software engineering. They will prove valuable when assessing technologies for use in a software architecture, or even when building your own tools. It also delves into considerations when making such decisions given the current state of an organization or project.

---
# Domains and Services

> A domain is the real-world subject area for which you’re architecting. A service is a set of functionality whose goal is to accomplish a task.

It is useful to first define which domains and services your architecture will encompass.

# Scalability & Designing for Failure
As far as planning for failure and architecting for scalability go, the following criteria should be considered:

- **Scalability**: Allows us to increase or decrease the capacity of a system to adhere to performance requirements in accordance with the demand.
- **Elasticity**: The ability of a system to scale dynamically; a highly elastic system can scale up or down automatically based on the current workload.
- **Availability**: The percentage of time a service or component is in an operational state.
- **Reliability**: The probability of a system in meeting its defined standards within a specified time interval.

## Scaling Methods
There are two types of scalability methods: vertical scaling, and horizontal scaling.

- **Vertical Scaling**:  focuses on adjusting the resources of a *single* machine to handle load, e.g., increasing the CPU, memory, disk, or I/O of a single machine.
- **Horizontal Scaling**: focuses on adjusting the *number* of machines in accordance with the load. These systems tend to be *distributed* or *decentralized*.

### Considerations
There are a few factors to consider when determining the scaling method of choice. Furthermore, there may also be cases to consider using *both vertical and horizontal scaling*:

- Scaling resource limitations on a single machine will determine the maximum amount of vertical scaling possible.
- Vertically scaled systems generally cannot offer high availability and reliability. Consider the following:
	- the effects of the machine dying, or a single component dying
	- backup and failover plans
- Horizontally scaled systems are adherent to the effects of the [CAP Theorem](CAP%20Theorem.md). Consider the trade-offs in consistency and availability that meet the technical requirements.

# Tight Versus Loose Coupling
Coupling refers to the amount of independence within your architecture's various domains, services and resources. Designing “good” architecture relies on trade-offs between the tight and loose coupling of domains and services.

> A **tightly coupled system** has extremely centralized dependencies and workflows. Every part of a domain and service is vitally dependent upon every other domain and service.

> A **loosely coupled system** has decentralized domains and services that do not have strict dependence on each other.

Due to the independent nature of loosely coupled systems, it is easy for software engineers to work in silos, building features that serve no value to other teams. To avoid this scenario, ensure common standards, ownership, responsibility, and accountability to the teams owning their respective domains and services. 

## Architecture Tiers
As you develop your architecture, it helps to be aware of architecture tiers. Your architecture has layers — data, application, business logic, presentation, and so forth — and you need to know how to decouple these layers.

There are *single tier* and *multitier* architectures.

**Single Tier**: In a single-tier architecture, your database and application are tightly coupled, residing on a single server. The tightly coupled nature of this architecture means that if a single component fails, the entire architecture fails. **Single-tier architectures offer simplicity but also severe limitations.** These are best suited for prototyping and development work, rather than for production systems.

**Multitier**: **The multitier architecture aims to decouple a single tier architecture to enable flexibility within your architecture.** A multitier (also known as n-tier) architecture is composed of separate layers: data, application, business logic, presentation, etc. These layers are bottom-up and hierarchical, meaning the lower layer isn’t necessarily dependent on the upper layers; the upper layers depend on the lower layers. The notion is to separate data from the application, and application from the presentation. Within each layer, you are free to use whatever technologies you prefer without the need to be monolithically focused.

# [Monoliths Versus Microservices](Monoliths%20Versus%20Microservices.md)

## Considerations for Architecture
It is suggested to pragmatically **use loose coupling as an ideal, while recognizing the state and limitations of the technologies currently used within your software architecture.** Incorporate reversible technology choices that allow for modularity and loose coupling whenever possible.

In short, monoliths offer simplicity at the cost of limitations on flexibility, while microservices offer flexibility at the cost of complexity. Consider the overhead and costs associated with each, and the long-term value that they will deliver in your architecture.

# Multitenancy
Multitenancy deals with the sharing of resources among teams, organizations and customers. It must be considered in an architecture to determine the level of security and isolation, and performance among its components.

There are two factors to consider in multitenancy: security and performance.

**Performance:** when sharing resources among tenants, ensure that you system can deliver consistent performance for all tenants under different loading scenarios. Avoid the *noisy neighbour problem*, where a single tenant may cause resource contention.

**Security:** data from different tenants must be isolated. Ensure that there is no data leakage.

# Event-Driven Architecture
The event-driven architecture acknowledges that the world, and by extension your business, is rarely static. It views things that happen as *events*, and makes information about those events available to different services within your architecture in an asynchronous manner.

An event-driven workflow encompasses the ability to create, update, and asynchronously move events across various parts of the data engineering lifecycle. This workflow boils down to three main areas: event production, routing, and consumption. An event must be produced and routed to something that consumes it without tightly coupled dependencies among the producer, event router, and consumer.

**The advantage of an event-driven architecture is that it distributes the state of an event across multiple services. This is helpful if a service goes offline, a node fails in a distributed system, or you’d like multiple consumers or services to access the same events.**

Anytime your architecture uses loosely coupled services, this is a candidate for event-driven architecture.

# Brownfield Versus Greenfield Projects
Before designing a software architecture, you need know if you're starting with a clean slate or redesigning an existing architecture.

> Projects roughly fall into two buckets: brownfield and greenfield. In either case, it is important to assess trade-offs, make flexible and reversible decisions, and always strive for a positive ROI.

## Brownfield Projects
Brownfield projects often involve refactoring and reorganizing an existing architecture and are constrained by the choices of the present and past.

They require a thorough understanding of the legacy architecture and the interplay of various old and new technologies. Rather than criticize prior architecture work, dig deep, ask questions, and understand *why* decisions were made.
### Strategies

> An architect's job is to make reversible, high-ROI decisions.

#### Direct Rewrite
In the direct rewrite strategy, architects jump headfirst into an all-at-once or big-bang overhaul of the old architecture, *figuring out deprecation as they go*. Though popular, **this is not an advisable approach due to the lack of planning, and may lead to many irreversible and costly decisions being made.**

#### Strangler Pattern
A popular alternative to a direct rewrite is the strangler pattern: new systems slowly and incrementally replace a legacy architecture’s components. Eventually, the legacy architecture is completely replaced. The attraction to the strangler pattern is its targeted and surgical approach of deprecating one piece of a system at a time. **This allows for flexible and reversible decisions while assessing the impact of the deprecation on dependent systems.**

## Greenfield Projects
Greenfield projects allow you to pioneer a fresh start, unconstrained by the history or legacy of a prior architecture.

With these project you have the **opportunity to try the latest and greatest tools and architectural patterns.** However, this comes with a **risk of getting carried away with *shiny object syndrome*.** Often, engineers may fall into the trap of the latest technology fad *without* understanding how it will impact the value of the project. There is also the notion of *resume-driven development*, wherein new technologies are stacked up without prioritizing the project's ultimate goals.

> Always prioritize requirements over building something cool.
