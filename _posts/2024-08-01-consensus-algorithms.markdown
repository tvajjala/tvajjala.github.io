---
layout: post
title:  "Distributed Consensus Algorithms"
date:   2024-08-01
description: Popular distributed consensus algorithms such as Paxos, Raft and ZAB 
---
> Consensus algorithms used in distributed systems to ensure that all
> processes agree on a single value.

  
- Paxos is fundamentally about reaching agreement in a network of unreliable components.
    -   It ensures that a single value is agreed upon among the participants, even if some of them fail.
-   Raft’s primary goal is to simplify the consensus process.
    -   It breaks down the process into smaller sub problems.
-   ZAB is about total order broadcast.
    -   It ensures all actions are executed in the same order across all nodes.

#### How it works

##### Paxos (Prepare Accept XO)

-   **Phases:** Paxos operates mainly in two phases — Prepare and Accept.
    -   The Prepare phase is about proposing a value, and the Accept phase is about agreeing on it.
-   **Multi-Paxos:** An optimization where one node remains the leader until it fails, reducing the number of messages.
    -   This is especially useful in systems where leadership changes are costly.
-   **Advantages:** Proven correctness and wide applicability.
    -   It’s a foundation for many other consensus algorithms.
-   **Disadvantages:** Its complexity makes it hard to implement and understand.
    -   Many systems opt for simpler algorithms due to this.

<span class="note">
Paxos protocol is named after a fictional legislative consensus system
on the Greek island of Paxos, which is known for its complex political
landscape.
</span>

##### Raft

-   Leader Election: Raft has a unique approach to leader election.
    -   A new leader is elected whenever the current one fails.
    -   This ensures system availability.
-   Log Replication: The leader is responsible for log replication.
    -   It ensures that all logs are consistent across nodes.
-   Advantages: Its main advantage is its simplicity.
    -   It’s easier to understand and implement than Paxos.
-   Disadvantages: Some argue it’s not as generalized as Paxos.
    -   However, its simplicity often outweighs this disadvantage.

##### ZAB (Zookeeper Atomic Broadcast)
-   Election Phase: A leader is elected.
    -   This is crucial for the subsequent phases.
-   Discovery Phase: The leader establishes synchronization with all followers.
    -   This ensures that all nodes start from a consistent state.
-   Broadcast Phase: The leader broadcasts client updates.
    -   This ensures that all nodes have the same data.
-   Advantages: Tailored for ZooKeeper’s needs, ensuring strong consistency.
-   Disadvantages: It’s specific to ZooKeeper’s use case.
    -   This might make it less suitable for other applications.

#### Real-life Use Cases
##### Paxos:
-   Distributed Databases: Systems like Google’s Spanner employ Paxos for global consistency.
    -   It ensures that data is consistent across global data centers.
-   Configuration Management: Chubby, a lock service by Google, uses Paxos.
    -   It ensures that configuration data is consistent.

Apache Cassandra uses Paxos, a consensus protocol, to achieve strong consistency. Paxos is also used in Cassandra for leader election

##### Raft:

-   Storage Systems: CockroachDB, a distributed SQL database, uses Raft.
    -   It ensures data consistency across nodes.
-   Service Orchestration: Kubernetes, the container orchestration system, employs etcd which uses Raft.
    -   It ensures that configuration data is consistent across nodes. 
    - Other systems that use Raft include Etcd, CockroachDB, and DynamoDB.

##### ZAB:

-   Distributed Coordination: Apache ZooKeeper, which uses ZAB, is pivotal for systems like Kafka.
    -   It ensures that nodes in a distributed system coordinate effectively.

##### References

-   <https://lamport.azurewebsites.net/pubs/paxos-simple.pdf>

-   <https://github.com/jguamie/system-design/blob/master/notes/raft-distributed-consensus.md>

-   <https://medium.com/@remisharoon/paxos-vs-raft-vs-zab-a-comprehensive-dive-into-distributed-consensus-protocols-6243a3f6539b>











