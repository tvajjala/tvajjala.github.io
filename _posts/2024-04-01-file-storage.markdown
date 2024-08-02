---
layout: post
title:  "File Storage System Design"
date:   2024-04-01
description: Distributed file storage services such as Dropbox/Google Drive System Design
---


**Table of content:**
- [Functional Requirements](#item-one)
- [Non Functional Requirements](#item-two)
- [Capacity Estimation](#item-three)
- [High Level System Design](#item-four)

> File Hosting Service like Dropbox enables users to store their data on cloud.
>These servers are maintained by cloud storage providers and made available to users over a network.


<a id="item-one"></a>
<h4><a href="1"></a> Functional Requirements</h4>

<ol>
<li>User should able to upload/download files</li> 
<li>System should sync files across all devices</li> 
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
<li>Read and Write heavy System</li>
<li>DAU : 1M users and 10 files upload/day</li> 
<li>100 uploads/sec</li> 

</ul>
<h6>Storage</h6>
<ul>
<li>100MB X10M -> 1000 TB/day - 1 Peta Byte/day</li> 
</ul>


<a id="item-four"></a>
<h4>High Level System Design </h4>

<figure>
	<img src="/assets/img/dropbox.png" alt=""> 
	<figcaption>Dropbox High Level System Design</figcaption>
</figure>


<ul>
<li>  Internal Metadata: Will keep track of all the files, chunks,  their versions and their location in the file system  </li>
<li>  Chunker split the files smaller pieces called chunks. it will also be responsible for reconstructing a file from its chunks.</li>
<li>  Watcher monitor the local workspace folders and notify the indexer of any file changes</li>
<li>  Indexer communicate with the remote synchronization service and internal metadata DB.</li>
</ul>
