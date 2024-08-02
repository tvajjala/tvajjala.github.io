---
layout: post
title:  "Video Calling Apps System Design"
date:   2023-12-31
image: direct-video-calling.png
description: Online video calling systems like Zoom/Skype
---


**Table of content:**
- [Functional Requirements](#item-one)
- [Non Functional Requirements](#item-two)
- [Capacity Estimation](#item-three)
- [High Level System Design](#item-four)
- [Algorithms](#item-five)

<p class="intro"><span class="dropcap">V</span>ideo Calling applications such as zoom/skype uses adaptive streaming to improve users realtime experience.


<a id="item-one"></a>
<h4><a href="1"></a> Functional Requirements</h4>

<ol>
<li>Video calling should support peer-to-peer and video conferences</li>
<li>System should support 300M video calls/day</li>
<li>System should support Adaptive streaming</li>
<li>System should adopt Scalable Video Coding</li>
</ol>

<a id="item-two"></a>
<h4>Non-Functional Requirements</h4>

<ol>
<li>System should be highly reliable and scalable</li>
<li>System should be highly available, loosing some frames is acceptable.</li>
</ol>

<a id="item-three"></a>
<h4><a href="3"></a> Capacity Estimation</h4>

<h6> Throughput </h6>
<ul>
<li>Throughput : 300M/10^5= 3000 Calls/sec.</li>
</ul>
<h6>Storage</h6>
<ul>
<li>Video recording stored in their local machines</li> 
</ul>


<a id="item-four"></a>
<h4>High Level System Design </h4>

<figure>
	<img src="/assets/img/zoom.png" alt=""> 
	<figcaption>Video Calling High Level System Design</figcaption>
</figure>



<h5>IMPORTANT NOTES</h5>
<ul>
<li>Adjusting resolution based on device type and bandwidth is called adaptive streaming.</li>
<li>Number of pixels in a video frame is called resolution</li>
<li> Sending many video streams for different resolutions isn’t scalable</li>
<li> System should use Scalable Video Coding (SVC) to stream video.</li>
</ul>



<p>
<a id="item-five"></a>
<h4> Algorithms </h4>

TBD