---
layout: post
title:  "Broadcasting Protocols"
date:   2024-07-31
description: Distributed System Broadcasting Protocols
---

### Broadcast Protocols

The popular message broadcasting techniques in a distributed system are the following:

-   point-to-point broadcast
-   eager reliable broadcast
-   gossip protocol

#### Point-To-Point Broadcast

-   The producer sends a message directly to the consumers in a point-to-point broadcast.
-   The retry mechanism on the producer and deduplication mechanism on the consumers makes the point-to-point broadcast reliable.
-   The messages will be lost when the producer and the consumer fail simultaneously

#### Eager Reliable Broadcast

-   Every node re-broadcasts the messages to every other node via reliable network links.
-   This approach provides improved fault tolerance because messages are not lost when both the producer and the consumer fail simultaneously.
-   The message will be re-broadcast by the remaining nodes.

#### Gossip Protocol

-   The gossip protocol is a decentralized peer-to-peer communication technique to transmit messages in an enormous distributed system
-   The key concept of gossip protocol is that every node periodically sends out a message to a subset of other random nodes.
-   The entire system will receive the particular message eventually with a high probability.
-   In layman’s terms, the gossip protocol is a technique for nodes to build a global map through limited local interactions
-   The gossip protocol is built on a robust, scalable, and eventually consistent algorithm. The gossip protocol is typically used to maintain the node membership list, achieve consensus, and fault detection in a distributed system
-   The gossip protocol is reliable because a node failure can be overcome by the retransmission of a message by another node.
-   Following mechanism can be implemented with gossip protocol
-   First-in-first-out (FIFO) broadcast.
-   causality broadcast.
-   total order broadcast.
-   The gossip protocol parameters such as `cycle` and `fanout` can be tuned to improve the probabilistic guarantees of the gossip protocol

### Types of Gossip Protocol

The time required by the gossip protocol to propagate a message across the system and the network traffic generated in propagating a message
must be taken into consideration while choosing the type of gossip protocol for a particular use case. The gossip protocol can be broadly categorized into the following types.
-   anti-entropy model
-   rumor-mongering model
-   aggregation model

### Anti-Entropy Model

> The anti-entropy algorithm was introduced to reduce the entropy
> between replicas of a stateful service such as the database.

-   This algorithm majorly used in databases to keep replicas consistent.
-   replicas are patched after comparing the datasets
-   The node with the newest message shares it with other nodes in every gossip round
-   The anti-entropy model usually transfers the whole dataset resulting in unnecessary bandwidth usage.
-   following techniques are used to identify the differences and send only delta which reduces bandwidth usage
-   checksum
-   recent update list,
-   Merkle tree
-   The anti-entropy gossip protocol will send an unbounded number of messages without termination
Data deduplication is a computing technique that removes duplicate copies of data from databases and data storage

### Rumor-Mongering Gossip Protocol
-   with this protocol only the latest updates are transferred across nodes
-   A message will be marked as removed after a few rounds of communication to limit the number of messages.

### Aggregation Gossip Protocol
The aggregation gossip protocol computes a system-wide aggregate by sampling information across every node and combining the values to
generate a system-wide value \[10\].

#### Gossip Protocol Performance
-   The number of nodes that will receive the message from a particular node is known as the `fanout`.
-   The count of gossip rounds required to spread a message across the entire cluster is known as the `cycle`
Cycles necessary to spread a message across the cluster = O(log n) to the base of fanout, where n = total number of nodes
-   Fanout 10
-   Total Nodes 1000

- Formula: log(1000) with base 10 → 3 Cycles

#### Gossip Protocol Use Cases
-   database replication
-   information dissemination
-   maintaining cluster membership
-   failure detection
-   generate aggregations (calculate average, maximum, sum)
-   generate overlay networks
-   leader election

#### System UseCases

-   Apache Cassandra employs the gossip protocol to maintain cluster membership, transfer node metadata (token assignment), repair unread data using Merkle trees, and node failure detection.
-   Consul utilizes the swim-gossip protocol variant for group membership, leader election, and failure detection of consul agents
-   CockroachDB operates the gossip protocol to propagate the node metadata
-   Hyperledger Fabric blockchain uses the gossip protocol for group membership and ledger metadata transfer
-   Riak utilizes the gossip protocol to transmit consistent hash ring state and node metadata around the cluster
-   Amazon S3 uses the gossip protocol to spread server state across the system
-   Amazon Dynamo employs the gossip protocol for failure detection, and keeping track of node membership
-   Redis cluster uses the gossip protocol to propagate the node metadata
-   Bitcoin uses the gossip protocol to spread the nonce value across the mining nodes

#### Reference

-   <https://highscalability.com/gossip-protocol-explained/>
