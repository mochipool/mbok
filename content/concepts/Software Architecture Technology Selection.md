---
date: 2025-03-18
draft: false
title: 'Software Architecture Technology Selection'
toc: true
---

# Preface
To preface, it is recommended to first design a good architecture before selecting technologies. Consider reading the [Principles of Good Software Architecture](Principles%20of%20Good%20Software%20Architecture.md) to gain a better understanding of what constitutes a good software architecture.

> Architecture is *strategic*, technology is *tactical*.

> Architecture defines the *what, why and when*, while tools are what make the architecture a reality; they are the *how*.

# Technology Selection
The following are some considerations for technology selection for your architecture:

- Team size and capabilities for managing the technology
- How it enables speed to market (time to value)
- Interoperability across your architecture stack
- Cost optimization and business value
- Immutable versus transitory technologies (how they stand up in the future)
- Deployment location (on-prem, cloud, hybrid cloud, multicloud)
- Benefits of building versus buying
- Monolith versus modular
- Serverless versus servers
- Optimization, performance and benchmarks

## Team Size and Capabilities
 A team’s size roughly determines the amount of bandwidth your team can dedicate to complex solutions. Especially for small teams or teams with weaker technical skills, **use as many managed and SaaS tools as possible, and dedicate your limited bandwidth to solving the complex problems that directly add value to the business.**
 
## Speed to Market

> Perfect is the enemy of good.

**Deliver value early and often; choose tools that help you move quickly, reliably, safely, and securely.** Avoid undifferentiated heavy lifting that engages your team in unnecessarily complex work that adds little to no value.

## Interoperability
Always be aware of how simple it will be to connect your various technologies across the software architecture. Design for modularity and give yourself the ability to easily swap out technologies as new practices and alternatives become available. Preferably use technologies which implement open standards.

## Cost Optimization and Business Value
Technology is a major cost driver, so your technology choices and management strategies will significantly impact your budget. There are three main lenses through which cost may be viewed: total cost of ownership, opportunity cost, and FinOps.

### Total Cost of Ownership
Total cost of ownership (TCO) is the total estimated cost of an initiative, including the direct and indirect costs of products and services utilized. Direct costs can be directly attributed to an initiative. Indirect costs, also known as overhead, are independent of the initiative and must be paid regardless of where they’re attributed.

How costs are paid also affect the way they are accounted for. There are two kinds of expenditures: *capital expenditure* and *operational expenditure*.

#### Capital Expenditure (CapEx)
Capital expenses, also known as capex, require an up-front investment. **It represents a significant capital outlay with a *long-term* plan to achieve a positive ROI on the effort and expense put forth.**

#### Operational Expenditure (OpEx)
Operational expenses, also known as opex, is gradual and spread out over time. **Whereas capex is long-term focused, *opex is short-term*. OpEx can be pay-as-you-go or similar and *allows a lot of flexibility*.** OpeEx is closer to a direct cost, making it easier to attribute to a project.

#### Recommendations
Engineers need to be pragmatic about flexibility. The technology landscape is changing too quickly to invest in long-term hardware that inevitably goes stale, can’t easily scale, and potentially hampers an engineer’s flexibility to try new things. **Given the upside for flexibility and low initial costs, it is suggested that engineers to take an opex-first approach centered on the cloud and flexible, pay-as-you-go technologies.**

### Opportunity Cost
Any choice inherently excludes other possibilities. Total opportunity cost of ownership (TOCO) is the cost of lost opportunities that we incur in choosing a technology, an architecture, or a process. **The goal is to minimize the TOCO.**

The first step to minimizing opportunity cost is evaluating it with eyes wide open. **How quickly and cheaply can you move to something newer and better? Make flexible and reversible technology choices.**

### [FinOps](FinOps.md)

## Immutable Versus Transitory Technologies
It’s all too easy to focus on a rapidly evolving future while ignoring the concrete needs of the present. Often times, building for future goals results in overarchitecting and overengineering, and yet the tooling chosen for the future may be out-of-date when this future arrives.

To circumvent such issues, **it is important to assess and understand **what is likely to change** and **what tends to stay the same**.**

We have two classes of tools to consider: immutable and transitory. 

### Immutable Technologies
Immutable technologies might be components that underpin the cloud or languages and paradigms that have stood the test of time. For languages, SQL and bash have been around for many decades, and it is unlikely that they will disappear anytime soon. Immutable technologies benefit from **the Lindy effect: the longer a technology has been established, the longer it will be used.**

**It is suggested to apply the Lindy effect as a litmus test to determine whether a technology is potentially immutable.**

### Transitory Technologies
Transitory technologies are those that come and go. The typical trajectory begins with a lot of hype, followed by meteoric growth in popularity, then a slow descent into obscurity. The JavaScript frontend landscape is a classic example.

### Recommendations
Given the rapid pace of technology change, **it is suggested to evaluate tooling every *two years*. Find the immutable technologies and use those as your base; transitory tools may then be built around them.** This way we have a solid a foundation as possible.

## Deployment Location
The principal places to run your technology stack are: on premises, the cloud, hybrid cloud, and multicloud.

### On Premises
On premises deployments typically require upfront capital expenditure to run. The advantage is that you own your hardware, and can potentially have a good ROI in the long-term. However, this comes with the inability to scale dynamically as your architecture requires, and upgrades can be costly and involve many headaches in migrating.

### Cloud
The cloud, on the other hand, enables this flexibility which enterprises usually seek in today's digital world. This however, comes at a higher price than if you were to own your equipment. Working with the cloud is about scalability, and indeed has the potential to earn a company more revenue with this potential to grow to the demands of more customers. There is a certain scale at which the cloud makes sense, and engineers must be able to optimize for the economics of the cloud with methods like [FinOps](FinOps.md).

### Hybrid Cloud
The hybrid cloud model assumes that an organization will indefinitely maintain some workloads outside the cloud. There are many reasons to consider a hybrid cloud model. Organizations may believe that they have achieved operational excellence in certain areas, such as their application stack and associated hardware. Thus, they may migrate only specific workloads where they see immediate benefits in the cloud environment.

### Recommendations

> Choose technologies for the present, but look toward the future.

Plan for the present. **Choose the best technologies for your current needs and concrete plans for the near future.** Choose your deployment platform based on real business needs while focusing on simplicity and flexibility.

On the other hand, **have an escape plan**; every technology, even open source ones, come with some degree of lock-in.

## Building Versus Buying

> Invest in building and customizing when doing so will provide a competitive advantage for your business. Otherwise, stand on the shoulders of giants and use what’s already available in the market.
 
Given the number of open source and paid services—both of which may have communities of volunteers or highly paid teams of amazing engineers—you’re foolish to build everything yourself.

### Open Source Software (OSS)
Open source software (OSS) is a software distribution model in which software, and the underlying codebase, is made available for general use, typically under specific licensing terms.

OSS has two main flavors: community managed and commercial OSS.

#### Community-Managed OSS
OSS projects succeed with a strong community and vibrant user base. Community-managed OSS is a prevalent path for OSS projects. The community opens up high rates of innovations and contributions from developers worldwide with popular OSS projects.

A common term used when evaluating community-managed OSS is *mindshare*. This essentially refers to the traction a project has, and how likely it is to have maintained support an utility for your use cases.

##### Evaluation Criteria
- Mindshare
- Maturity
- Troubleshooting experience
- Project management process
	- How difficult is it to submit an issue, and get it resolved?
- Team
- Developer relations and community management
- Contributions
- Roadmap
- Self-hosting and maintenance

#### Commercial OSS
Sometimes OSS has some drawbacks. Namely, you have to host and maintain the solution in your environment. This may be trivial or extremely complicated and cumbersome, depending on the OSS application. Commercial vendors try to solve this management headache by hosting and managing the OSS solution for you, typically as a cloud SaaS offering.

##### Evaluation Criteria
- Value as opposed to self-hosting
- Delivery model
	- How easy is it to get the latest version
- Support
- Release schedule and bug fixes
- Company finances
	- Is the company viable? Will they still be in business in a couple of years?
- Logos versus revenue
	- Is the company focused on growing the number of customers (logos), or is it trying to grow revenue? You may be surprised by the number of companies primarily concerned with growing their customer count, GitHub stars, or Slack channel membership without the revenue to establish sound finances.
- Community support
	- Is the company truly supporting the community version of the OSS project? How much is the company contributing to the community OSS codebase? Controversies have arisen with certain vendors co-opting OSS projects and subsequently providing little value back to the community. How likely will the product remain viable as a community-supported open source if the company shuts down?
	
### Proprietary Software
While OSS is ubiquitous, a big market also exists for non-OSS technologies. Although you won’t have the transparency of a pure OSS solution, a proprietary independent solution can work quite well, especially as a fully managed service in the cloud.

#### Evaluation Criteria
Consider the following when evaluating proprietary software offerings:
- Interoperability
- Mindshare and market share
- Documentation and support
- Pricing
	- Is the pricing understandable? Map out low-, medium-, and high-probability usage scenarios, with respective costs.
- Longevity
	- Will the company survive long enough for you to get value from its product?

### Recommendations

>  As the old saying goes, time kills deals.

Build versus buy comes back to **knowing your competitive advantage and where it makes sense to invest resources toward customization.** **In general, favor OSS and commercial OSS by default, which frees you to focus on improving those areas where these options are insufficient. Focus on a few areas where building something will add significant value or reduce friction substantially.**

## Monoliths Versus Microservices
Read the document [Monoliths Versus Microservices](Monoliths%20Versus%20Microservices.md) for an overview on this concept.

### Recommendations
When evaluating whether to use a monolithic or modular technology, assess the following criteria:

- Interoperability
- Ability to make reversible decisions (i.e. rollback and/or switch out the technology as necessary); in a monolith, it is usually more difficult to escape the ecosystem, since everything is tightly coupled.

## Servers Versus Serverless
A big trend for cloud providers is serverless, allowing developers and engineers to run applications without managing servers behind the scenes. Serverless provides a quick **time to value** for the right use cases. For other cases, it might not be a good fit.

### Serverless
The main reasons for the popularity of serverless are cost and convenience. Instead of paying the cost of a server, you pay only when your code is evoked. As such, engineers would do well to understand the details of cloud pricing to predict when serverless deployments will become expensive. However, serverless functions suffer from an inherent overhead inefficiency. Handling one event per function call at a high event rate can be catastrophically expensive.

#### Suggestions
Monitor your serverless infrastructure to determine cost per event in a real-world environment, and model using this cost per event to determine overall costs as event rates grow. Modeling should also include worst-case scenarios, for e.g., in the case a site gets hit by a bot swarm or DDoS attack.

### Servers
There are a two main reasons why you'd want to run your own servers:

- **Cost**: Serverless makes less sense when the usage and cost exceed the ongoing cost of running and maintaining a server. This is typically found under lower usage scenarios; for smaller-scale operations running a server just might cost less.
- **Customization**: Customization, power, and control are other major reasons to favor servers over serverless. Some serverless frameworks can be underpowered or limited for certain use cases.

#### Suggestions
There are some things to consider when using servers, particularly in the cloud, where server resources are ephemeral:

- Expect servers to fail
	- Treat each server as an ephemeral resource, and avoid over-reliance and over-customization of your server.
- Employ Infrastructure-as-Code (IaC) principles and automation to quickly bootstrap new servers when needed.
- In cloud environments, use clusters and autoscaling to automatically scale your servers to the required demand.
- When applications have many dependencies, consider using container frameworks to isolate each workload.

## Optimization, Performance and Benchmarks
One common marketing ploy used by companies to prop their product is to use benchmarks against competitors in the space. However, these benchmarks tend to make comparisons against tooling that are *completely optimized for different use cases*, or use test scenarios that bear no resemblance to real-world needs.

> Remember, tools serve a purpose. Do your own research, and always make sure that the benchmarks are relevant to your use-case.
