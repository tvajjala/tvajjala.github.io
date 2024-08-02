---
layout: post
title:  "URL Shortener System Design"
date:   2023-05-30
description: URL shortening is used to create shorter aliases for long URLs.
---



**Table of content:**
- [Functional Requirements](#item-one)
- [Non Functional Requirements](#item-two)
- [Capacity Estimation](#item-three)
- [High Level System Design](#item-four)


>URL shortening is used to create shorter aliases for long URLs.

#### Functional Requirements

1. Given a URL, our service should generate a shorter and unique alias of it.
2. When users access a short link, our service should redirect them to the original link.
3. Users should optionally be able to pick a custom short link for their URL.
4. Links will expire after a standard default timespan. Users should be able to specify the expiration time.

#### Non-Functional Requirements:
1. The system should be highly available.
2. URL redirection should happen in real-time with minimal latency.
3. Shortened links should not be guessable (not predictable).

#### Capacity Estimation
1. Read heavy system 1:100 write read ration

#### High Level Design

1. Compute hash using MD5/ SHA256 of the given URL.
2. Encode the hash using base62 , base36
3. ShortURL key length will be 6-10 characters. `Ex: tinyurl.com/abcdefgh`
4. If we are using base62 encoding . `62^10 = 65 Billion`
5. Encoded string generates 21 character string. we need to take 6 chars from them as random.


<figure>
	<img src="/assets/img/url_shortner.png" alt=""> 
	<figcaption>URLShortner High Level System Design</figcaption>
</figure>


##### KGS(Key Generation Service)
- With above approach, there is a possibility of key duplication.
- KGS will make sure all the keys inserted into key-DB are unique.
- KGS can use two tables to store keys:
  - one for keys that are not used yet, and one for all the used keys.
  - As soon as KGS gives keys to one of the servers, it can move them to the used keys table.
- KGS can always keep some keys in memory to quickly provide them whenever a server needs them.

##### Partition

1. Range based partitioning
2. Hash based partitioning

#### Algorithms

Following algorithms used in URL Shortening service.

##### LRU Cache

Using LinkedHashMap to create caching that gives most recently used entries


{%- highlight python -%}

from collections import OrderedDict
import threading
class LRUCache:

    def __init__(self, capacity):  # size of the cache entries
        self.capacity = capacity
        self.cache = OrderedDict()
        self.lock = threading.Lock()

    def put(self, key, value):
        self.lock.acquire()
        self.cache[key] = CacheElement(key, value)
        self.cache.move_to_end(key)
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False) # pop item last=False means remove from left
        self.lock.release()

    def get(self, key):

        if key not in self.cache:
            print("return -1")
            return -1
            #  raise Exception("Entry Not found")
        self.cache.move_to_end(key)
        # if creation time older than 1 hr 10 , 12-1
        print(f"Returning {key}")
        return self.cache[key]
{%- endhighlight -%}

##### Encoding

{%- highlight python -%}
def base_encode(input):
    map = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
    shortURL = ""
    length = 62
    while input > 0:
        shortURL += map[input % length]
        input // length
    return shortURL
{%- endhighlight -%}
