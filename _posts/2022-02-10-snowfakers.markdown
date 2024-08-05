---
layout: post
title:  "How Snowflake Ids are unique"
date:   2022-02-10
description: Snowflake IDs, also known as snowflakes, are a type of unique identifier used in distributed computing to create time-ordered IDs
---

#### What are Snowflake IDs

Snowflake IDs, also known as snowflakes, are a type of unique identifier used in distributed computing to create time-ordered IDs. 

Twitter (now X) created the format and uses it for tweet IDs, but other companies, such as Discord, Instagram, and Mastodon, have also adopted it


##### How they are unique

Snowflake IDs are made up of multiple components, including:


- Timestamp 
  - The current time in milliseconds, which ensures that IDs generated at different nodes are roughly ordered.
- Node identifier
  - A unique identifier for the node (machine or server) generating the ID, which helps prevent collisions in distributed systems.
- Sequence number
  - A counter that starts at 0 and increments with each ID generated, which resolves conflicts when multiple IDs are generated at the same timestamp 


> Snowflake IDs are 64-bit long unsigned integers, which provides a large space for unique identifiers. With default settings, a snowflake generator can generate up to 4,096 unique IDs per millisecond, which is the maximum that the format supports