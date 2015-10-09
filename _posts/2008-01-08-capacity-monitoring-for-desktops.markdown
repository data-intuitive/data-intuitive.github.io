---
author: Toni
comments: true
date: 2008-01-08 16:26:00+00:00
layout: post
slug: capacity-monitoring-for-desktops
title: Capacity Monitoring for Desktops?
wordpress_id: 61
tags:
- Capacity
- Monitoring
- Performance
- VDI
- VMware
---

With the rise of VDI (Virtual Desktop Infrastructure, [see here for a comprehensive overview](http://www.brianmadden.com/content/article/Virtual-Desktop-Infrastructures-VDI-Whats-real-today-whats-not-and-whats-needed)) and the momentum it has, one starts to ask similar questions as with conventional server consolidation: what type of virtualization platform is required, how many users/desktops can I host, will there still be room for scaling, etc.

 

The way to approach this in server virtualization projects is by means of capacity monitoring and planning using virtualization scenarios. We refer to [earlier](http://verbeiren.blogspot.com/2007/09/vmware-capacity-planner-taking-data.html) [posts](http://verbeiren.blogspot.com/2007/12/capacity-planning-what-to-monitor-and.html) for more information about this topic. 

 

The question we are asking: can we use the same concepts and ideas for desktop virtualization? My answer is 'NO', because:

 

  
  1. A user acts completely different than a process or service: less predictable, depending on our mood, depending on the time of the day, etc.
   
  2. Some end-user applications ask 1OO% of the CPU even while they are not doing anything. The classic example used to be the game 'Pinball'. Even a screensaver can take a large amount of CPU power. 
   
  3. In a VDI context, this becomes even more important. For instance: why would you scale your virtual desktop CPU and memory to include desktop search if really nothing personal can be found on the hosted desktop?
   
  4. When starting and running 10 applications at the same time, we will probably only use 5 of them later, but still... they require CPU power (and memory) while seeming idle.
   
  5. If a user has meetings half the time, does that mean his session is closed? Does it still require processing power? How can this be analyzed?
   
  6. Etc.
 

In other words, a desktop environment is inherently different from a server environment. This is why in my opinion it is harder to maintain a Citrix farm than a VMware farm: applications and users tend to be less predictable and 'stable' than servers.

 

Does that mean that we can not do any sizing or planning in a VDI context? On the contrary, we should only keep in mind that applying exactly the same reasoning as with server consolidation planning is not a good idea. 

 

A few more tips:

 

  
  * Make sure you have an overview of running processes and their CPU/memory utilization. This helps in deciding what is really important.
   
  * Be careful with averages and peaks: a PC that is running all the time will have a low average, but may be used heavily during the day and a PC may be 100% used during the day because of some applications.
   
  * Take into account inactive time during the day.
   
  * Do not try to analyze the 'average' user, instead create classes (say 5 or so) that each have typical characteristics. Use these classes to create the virtualization scenarios.
