---
layout: post
title:  "Logical Clocks"
date:   2024-02-10
description: Logical clocks are used in distributed systems to order events.
---
> Logical clocks are useful in computation analysis, distributed algorithm design, individual event tracking, and exploring computational progress.

#### Type of Logical Clocks

* Lamport Clocks - which are monotonically increasing software counters
* Vector Clocks - allow for partial ordering of events in a distributed system.
* Version Vectors -  order replicas, according to updates, in an optimistic replicated system
* Matrix Clocks - an extension of vector clocks that also contains information about other processes' views of the system
