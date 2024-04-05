---
description: They are used for parallel programing.
---

# MPI and OpenMP

### Slight Difference

* **OpenMP** is an API that makes it (presumably) easier to write shared-memory multi-processing programs.
* **MPI** stands for Message Passing Interface. It is a set of API declarations on message passing (such as send, receive, broadcast, etc.).
  * The idea of "message passing" is relatively abstract. It could mean passing messages between local processes or processes distributed across networked hosts, etc. Modern implementations try very hard to be versatile and abstract away the multiple underlying mechanisms (shared memory access, network IO, etc.).
