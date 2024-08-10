---
layout: post
title:  "Chaos Engineering"
date:   2024-02-10
description: To build resilient distributed systems
---

> Observing a distributed system's behavior in a controlled experiment is called chaos engineering.


###  Netflix Chaos Engineering

Netflix created a tool to randomly shut down servers and called it `chaos monkey`:

* Read information about server nodes via the continuous delivery platform
* It interacts via the continuous delivery platform to kill server nodes

Then they check if traffic gets routed to another server without affecting users.


#### how they do chaos engineering:

1. Create a hypothesis about how the system will behave during a failure
2. Run a small test to introduce failure - switch off the server or change the network configuration
3. Observe the system’s behavior & measure the failure impact
4. Automate fix for the problem.

#### Benefits

* Run Canaries on production environment by introducing failures
* Evaluate impact & frequency - server crash, latency, response time
* Minimize blast radius that helps to avoid real failures.

