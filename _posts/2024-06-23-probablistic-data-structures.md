---
layout: post
title:  "Probabilistic Data Structures"
date:   2024-06-23
description: Trade accuracy for efficiency and scalability,consuming less memory and computational resources than deterministic alternatives
---

> Probabilistic data structures can enable fast, scalable, and low-memory data processing
for real-time analytics

##### Bloom filters

A Bloom filter is one of the probabilistic data structures supported by Redis Stack and is used to test whether an item is a member of a set.

1. It is crucial as a data deduplication solution – that is, for removing duplicated data from a set.
2. It is a memory-efficient and fast data structure that uses a bit array and a set of hash functions to determine whether an item is in the set or not.
3. A Bloom filter simplifies the management and speed of solutions that require the existence or membership verification.


Some other scenarios where Bloom filters represent an efficient solution are as follows:

* **_User_registration:_** Blooms filters can be used to verify user existence without hitting database.
* **_Spam filtering:_** Maintaining a list of malicious URLs or IPs to prevent spam or fraud.
* **_Fraud detection:_** Checking whether a credit card number belongs to a list of blocked or suspicious credit cards (stolen or cloned). This is particularly useful because such a filter could also be shared between financial institutions without the risk of storing the number in clear text.
* **_Suspicious activity:_** Verifying user activity (geographical location, date and time of activity, category of a product being purchased, and so on) and preventing authentication or allowing certain operations until authentication or verification is completed using a stronger method.
* **_Ad placement and recommendations:_** Using the Bloom filter, you can answer questions such as “Has the user seen this ad?” and then act accordingly.
* **_Spell-checking:_** If a word does not belong to a filter, it is misspelled.

##### TOP-K

The `Top-K` data structure is used to keep track of items with the highest rank, such as the top players in a leaderboard.
The ranking, or score, is often based on the count of how many times an item appears in the data source (such as a stream), making the data structure ideal for identifying elements with the highest frequency.
Among the most common use cases of this data structure are leaderboards, trending entities in a system, detecting network anomalies, and DDoS attacks.


Similar to Cuckoo filters, `Top-K` uses buckets to store fingerprints and counters.
This method employs a two-dimensional array characterized by its width and depth:

* `width` represents the number of buckets within each array
* `depth` signifies the number of arrays or hash functions employed

##### Cuckoo filters

Cuckoo filters are an evolution of Bloom filters that were published in 2014 and address the limitations of Bloom filters, especially around collision handling.

"`This filter inherits its name from the cuckoo bird, famous for laying its eggs in the nests of other bird species and leaving them to be raised by the host bird. In doing so, the cuckoo pushes the other eggs or chicks out of the nest.`"

Cuckoo filters use a fingerprint-based technique that allows for the fast and efficient handling of collisions and reduces the rate of false positives while maintaining the same space requirements as Bloom filters.


Instead of storing the hashed version of an item as Bloom filters do, Cuckoo filters use multiple locations, or buckets, to store the fingerprint representation of the item. When a new item is added to the filter and a collision occurs at a candidate bucket, the existing item is moved to another candidate bucket. If that bucket is also occupied, the filter keeps searching until a bucket without the fingerprint is found or the filter reaches the maximum number of attempts to kick out existing items. This approach reduces the rate of false positives while maintaining the same space requirements as Bloom filters.

##### Count-Min sketch

The Count-Min sketch probabilistic data structure, like HyperLogLog, counts the items that have been added,
with the difference that the Count-Min sketch counts the number of times specific items have been added – that is, their frequency.

When using a Count-Min sketch data structure, any frequency counts below a predetermined threshold (established by the error rate) should be disregarded.
The Count-Min sketch serves as a valuable tool for counting element frequencies in a data stream, especially when dealing with higher counts.


##### HeavyKeeper

Collisions can be avoided using the HeavyKeeper algorithm, which relies on exponential decay.
When a hash collision occurs (two elements compete for the same bucket),
the algorithm initiates a reduction in the counter of the current occupant of the bucket.
However, this reduction does not occur with every collision.

##### T-digest

t-digest is a data structure for estimating quantiles from a data stream or a large dataset using a compact sketch.

##### HyperLogLog

HyperLogLog is an efficient solution to count the number of unique occurrences in a set, which, in practice, is the cardinality of the set.

This is especially useful when accuracy is not required: the count is probabilistic but presents a very low error.

HyperLogLog does not store any information as the items that are added pass through a hashing function, so it is not possible to remove elements once they are counted.

HyperLogLog is the simplest probabilistic data structure and using it is as easy as adding elements to it using the PFADD command:

count unique items in a set using up to 12 KB of memory and with good approximation (with a standard error of 0.81%), let’s discover how to verify whether an item belongs to a set.
For that, we will use the Bloom filter.


### Reference 

