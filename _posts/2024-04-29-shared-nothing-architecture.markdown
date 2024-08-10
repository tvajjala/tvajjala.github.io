---
layout: post
title:  "Shared Nothing Architecture"
date:   2024-04-29
description: Shared nothing architecture provides low latency, high bandwidth, as well as high availability.
---

> Shared nothing architecture provides low latency, high bandwidth, as well as high availability.


#### Popular Architectures for high transaction rate systems


The three most commonly mentioned architectures for multiprocessor high transaction rate systems are:

<ul>
<li> <b>Shared memory (SM)</b>, i.e. multiple processors shared a common central memory</li>
<li> <b>Shared disk (SD)</b>, i.e. multiple processors each with private memory share a common collection of disks</li>
<li> <b>Shared nothing (SN)</b>, i.e. neither memory nor peripheral storage is shared among processors</li>
</ul>

#### ScyllaDB

* ScyllaDB is the monstrously fast and scalable NoSQL database. Fully compatible with apache Cassandra and Amazon DynamoDB,
* ScyllaDB embraces a shared-nothing approach that increases throughput and storage capacity as much as 10X that of Cassandra.
*  Comcast, Medium, Starbucks, Ola Cabs Adopted ScyllaDB to realize order-of-magnitude performance improvements and reduce hardware costs

#### Why Discord migrated from Cassandra to ScyllaDB

Cassandra is a LSM Based data store, reads are more expensive than writes. Writes are appended to a commit log and written to an in memory structure called a `memtable` that is eventually flushed to disk. 
Reads, however, need to query the `memtable` and potentially multiple SSTables (on-disk files), a more expensive operation. 

Read this [blog](https://discord.com/blog/how-discord-stores-trillions-of-messages) how discord migrated to ScyllaDB to improve performance and lower latency levels.




#### Reference

-  [https://www.scylladb.com/glossary/shared-nothing-architecture/](https://www.scylladb.com/glossary/shared-nothing-architecture/)
-  [https://discord.com/blog/how-discord-stores-trillions-of-messages](https://discord.com/blog/how-discord-stores-trillions-of-messages)
