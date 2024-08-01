---
layout: post
title:  "Video Streaming System Design"
date:   2024-06-31
description: YouTube or NetFlix System Design 
---




<p class="intro"><span class="dropcap">Y</span>ouTube  looks simple: content creators upload videos and viewers click play. 
Is it really that simple? Not really. There are lots of complex technologies underneath the simplicity.


<h4> Functional Requirements</h4>

<ol>
<li>User should be able to upload and watch videos</li> 
<li>System should support different video formats</li> 
<li>System should recommend videos to viewers</li> 
</ol>

<h4> Non-Functional Requirements</h4>

<ol>
<li>System should highly reliable/scalable</li> 
<li>System should be highly available with eventual consistency</li> 
</ol>

<h4> Capacity Estimation</h4>

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


<figure>
	<img src="/assets/img/youtube-system-design.png" alt=""> 
	<figcaption>Video Streaming High Level System Design Components</figcaption>
</figure>

<h4>Low Level Component Design </h4>


User uploads videos into object storage, transcoder queue process them asynchronously and encodes into different format.
Different video formats make it available to CDN to improve view experience.
Metadata stored into Cassandra database.
video recommendation service user two -tower approach to generation video recommendations.




<h4> Recommendation Top K Movies </h4>



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