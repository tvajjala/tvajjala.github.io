---
layout: post
title:  "Messenger App System Design"
date:   2023-02-10
description: Messaging systems like WhatsApp/Facebook Messenger
---


**Table of content:**
- [Functional Requirements](#item-one)
- [Non Functional Requirements](#item-two)
- [Capacity Estimation](#item-three)
- [High Level System Design](#item-four)
- [Algorithms](#item-five)

<p class="intro"><span class="dropcap">M</span>essaging applications such as WhatsApp/Facebook Messengers provide instant messaging services to users. 


<a id="item-one"></a>
<h4><a href="1"></a> Functional Requirements</h4>

<ol>
<li>System should be able to support one-to-one/group messaging</li> 
<li>Users should be able to see live status</li> 
<li>System should support file sharing(on receive deletion)</li> 
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
<li>DAU : 50M users and each user watch 10 messages/day</li> 
<li> 500 million messages/day -> 5000 RPS</li> 
<li>10% of users upload files->  50 million files/day</li> 
</ul>
<h6>Storage</h6>
<ul>
<li>50 M X100 = 5GB/day</li> 
</ul>


<a id="item-four"></a>
<h4>High Level System Design </h4>

<figure>
	<img src="/assets/img/whatsApp.png" alt=""> 
	<figcaption>WhatsApp High Level System Design</figcaption>
</figure>


<ul>
<li> User send messages to user/group which is handled by chat server</li>
<li> Chat server extracts files (if any) upload into media storage.</li>
<li> Event triggered message queue and notification send to user/group via notification server</li>
<li> Presence server uses heartbeat protocol to check whether user active/not </li>
<li> Communication between chatServer and user happens through WebSocket(Duplex)/ SSE/Long Polling</li>
</ul>


<p>
<a id="item-five"></a>
<h4> Algorithms </h4>

<ul>
<li> WebSockets</li>
<li> Server Sent Events</li>
<li> Long Polling</li>
<li> HeartBeat Protocols</li>
</ul>