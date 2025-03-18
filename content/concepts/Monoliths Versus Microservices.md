---
date: 2025-03-17
draft: false
title: 'Monoliths Versus Microservices'
---

# Monoliths Versus Microservices
The monolith camp favors the simplicity of having everything in one place. It’s easier to reason about a single entity, and you can move faster because there are fewer moving parts. The microservices camp leans toward decoupled, best-of-breed technologies performing tasks at which they are uniquely great. Especially given the rate of change in products in the technology world, the argument is **you should aim for interoperability among an ever-changing array of solutions.**

## Monoliths
The general notion of a monolith is to include as much as possible under one roof; as such components within a monolith tend to be tightly coupled. Coupling within a monolith can be viewed in two ways: *technical coupling* and *domain coupling*. *Technical coupling* refers to architectural tiers, while *domain coupling* refers to the way domains are coupled together.

Due to the tightly coupled nature of components in a monolith, reusing components across the architecture is difficult or impossible.

### Advantages
- The pros of the monolith are it’s easy to reason about, and it requires a lower cognitive burden and context switching since everything is self-contained.

### Disadvantages
- User-induced problems can happen with monoliths. For example, in a monolithic ETL pipeline that takes 48 hours to run, if anything breaks anywhere in the pipeline, the entire process may have to restart.
- Multitenancy in a monolithic system can also be a challenging issue; isolating workloads may not be trivial.
- Conflicts between dependencies and resource contention are frequent sources of headaches. For e.g., in Airflow, an application requiring a specific version of one package may conflict with another application that requires a lower version.
- Switching to a new system will be painful if the vendor or open source project dies. Because all of your processes are contained in the monolith, extracting yourself out of that system, and onto a new platform, will be costly in both time and money.

## Microservices
Microservices architecture comprises separate, decentralized, and loosely coupled services. Each service has a specific function and is decoupled from other services operating within its domain. If one service temporarily goes down, it won’t affect the ability of other services to continue functioning.

### Advantages
- Modularity allows engineers to choose the best technology for each job or step along the pipeline.

### Disadvantages
- There is more to reason about as compared to monolithic systems.
- Orchestration is required to connect all the different components together in a modular system.

## Distributed Monoliths
The distributed monolith pattern is a distributed architecture that still suffers from many of the limitations of monolithic architecture. The basic idea is that one runs a distributed system with different services to perform different tasks. Still, services and nodes share a common set of dependencies or a common codebase. This potentially enables the system to scale to more load, but again consideration must be made for the drawbacks like dependency conflicts.
