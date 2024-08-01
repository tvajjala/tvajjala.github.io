---
layout: post
title:  "Video Streaming System Design"
date:   2024-06-31
description: Popular streaming services such as YouTube/Netflix/Hulu helps to upload and stream videos.
---

**Table of content:**
- [Functional Requirements](#item-one)
- [Non Functional Requirements](#item-two)
- [Capacity Estimation](#item-three)
- [High Level System Design](#item-four)
- [Algorithms](#item-five)

<p class="intro"><span class="dropcap">Y</span>ouTube or Netflix are popular video streaming services.
These services allow users to upload / stream /share videos.


<a id="item-one"></a>
<h4><a href="1"></a> Functional Requirements</h4>

<ol>
<li>User should be able to upload and stream videos</li> 
<li>System should support different video formats</li> 
<li>System should recommend videos to viewers</li> 
</ol>

<a id="item-two"></a>
<h4>Non-Functional Requirements</h4>

<ol>
<li>System should highly reliable/scalable</li> 
<li>System should be highly available with eventual consistency</li> 
</ol>

<a id="item-three"></a>
<h4><a href="3"></a> Capacity Estimation</h4>

<h6> Throughput </h6>
<ul>
<li>DAU : 5M users and each user watch 5 video/day</li> 
<li>25Million views/day->  250 Views/sec(RPS)</li> 
<li>10% of users upload->  5 videos/sec</li> 
</ul>
<h6>Storage</h6>
<ul>
<li>5M X 500MB= 250 TB/day</li> 
</ul>


<a id="item-four"></a>
<h4>High Level System Design </h4>

<figure>
	<img src="/assets/img/youtube-system-design.png" alt="" width="70%"> 
	<figcaption>Video Streaming High Level System Design Components</figcaption>
</figure>


<ul>
<li>  User uploads videos into object storage and updates medata into database(Cassandra) </li>
<li>  Transcoder service will read from queue process them asynchronously and encodes into different format.</li>
<li>  Different video formats make it available to CDN to improve view experience.</li>
<li>  Video recommendation service uses two-tower approach to generation video recommendations.</li>
<li>  Client stream videos on their devices using different streaming protocols such as Apple HTTP Live/MPEG.</li>
</ul>


<p>
<a id="item-five"></a>
<h4> Algorithms </h4>
<p>
Below algorithms helps to find top K movie recommendation using Heap DataStructure.
</p>

<span style="font-size:0.7em;width: 60%">

{%- highlight python -%}
from heapq import *

class ListNode:
def __init__(self, val=0, nextNode=None):
self.val= val
self.next = nextNode


def topKMovies(arrays):
heap = []
for head in arrays:
heappush(heap, (head.val, head))

    topMovies = []
    while heap:
        nodeVal, node = heappop(heap)
        topMovies.append(nodeVal)
        if node.next:
            heappush(heap, (node.next.val, node.next))
    
    return topMovies

if __name__=="__main__":

    n1 = ListNode(1, ListNode(5, ListNode(7, None)))
    n2 = ListNode(2, ListNode(4, ListNode(8, None)))
    array = [n1, n2]
    print(topKMovies(array))

{%- endhighlight -%}
</span>
