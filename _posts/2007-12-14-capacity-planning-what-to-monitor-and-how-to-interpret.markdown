---
author: Toni
comments: true
date: 2007-12-14 14:35:00+00:00
layout: post
slug: capacity-planning-what-to-monitor-and-how-to-interpret
title: 'Capacity Planning: What to monitor and how to interpret'
wordpress_id: 55
tags:
- Capacity
- Monitoring
- Performance
---

Capacity planning starts with capacity (of performance) monitoring.  
  
Everybody who is involved in the monitoring of systems will acknowledge that the most difficult aspects in monitoring a server (or set of servers) are:  


  

  1. Finding the proper indicators for the performance of the system (CPU usage, CPU cycles, memory usage, paging, etc.)
  

  2. Making sure they are queried regularly, but not too much in order to avoid impacting the performance of the system by monitoring it.
  

  3. Storing the resulting data
  

  4. Summarize, create views, average, etc. (this also depends on what you want to know about the system)
  

  5. Analyze, interpret, etc.
  
  
Did I say the most difficult aspects? Are there any other aspects? Well, not really... capacity monitoring (and planning as a further step) is not an easy task:  


  

  * Are you aware of the utilization of your systems?  Even of your workstations?
  

  * Would you have any idea how many of your servers could be placed on a virtualization platform with a specific set of hardware characteristics?
  

  * Would you know when your mail server had the hardest time managing mail boxes the last couple of weeks?
  
  
Probably the answer is 'no'. Maybe the answer is 'I don't care'?   
  
Most companies do care, because of several reasons: cost, manageability, flexibility, scalability, environment, space, etc.  
  
There are already some players on the market: VMware Capacity Planner (see earlier posts), PlateSpin PowerRecon, Veeam Monitor, etc.  I'm mostly used to VMware Capacity Planner (VMCP) but recently, I have also evaluated both PowerRecon and Veeam Monitor. More about this later.
