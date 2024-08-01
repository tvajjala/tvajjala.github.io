---
layout: post
title:  "Web Crawler System Design"
date:   2024-06-12
description: Web Crawler System Design 
---


<h4> Functional Requirements</h4>

<ol>
<li>System should download and validate pages</li> 
<li>System should able to generate mirror site</li> 
<li>System should identify copyright infringements</li> 
<li>Restrict crawling per /robots.txt</li> 
</ol>

<h4> Non-Functional Requirements</h4>

<ol>
<li>System should highly reliable/scalable</li> 
<li>System should be highly available with eventual consistency</li> 
</ol>

<h4> Capacity Estimation</h4>

<h6> Throughput </h6>
<ul>
<li>DAU :10M pages/day -> 100 pages/sec</li> 
</ul>
<h6>Storage</h6>
<ul>
<li>100KBX10M -> 1GB/day</li> 
</ul>




<figure>
	<img src="/assets/img/web_crawler.png" alt=""> 
	<figcaption>WebCrawler High Level System Design Components</figcaption>
</figure>


