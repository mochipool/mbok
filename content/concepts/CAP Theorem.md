---
date: 2025-03-12
draft: false
title: 'Cap Theorem'
---
### CAP Theorem:
> The CAP theorem states that in a distributed data store, you can only guarantee two out of the following three properties: consistency, availability, and partition tolerance. In reality, partition tolerance is a requirement, and therefore during a network failure, a system must choose between providing consistent data or being available to respond to requests.

- **Consistency**: Every read from the database gets the latest (and correct) piece of data or an error
- **Availability**: Every request is received and a response is given -- without a guarantee that the data is the latest update
- **Partition Tolerance**: The system continues to work regardless of losing network connectivity between nodes
