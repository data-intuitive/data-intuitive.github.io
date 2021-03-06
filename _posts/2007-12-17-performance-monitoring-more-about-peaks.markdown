---
author: Toni
comments: true
date: 2007-12-17 14:51:00+00:00
layout: post
slug: performance-monitoring-more-about-peaks
title: 'Performance Monitoring: More about Peaks'
wordpress_id: 57
tags:
- Capacity
- Monitoring
- Performance
---

In a previous post, we talked about averages (types of averages) and peaks and how peaks can tell you something about the spreading (variance, standard deviation) of the data.  
  
Information about peaks is required (especially in capacity planning situations) to understand the sizing of the platform you're running on. On the other hand, having a peak utilization of (say) 80% and an average of 20% still does not tell you that much: how long was the system running at high CPU levels? Maybe only for 10 seconds during the day (a scheduled database operation, backup procedures, etc.)? Is it crucial for our service that this high level of CPU can be guaranteed at that moment, or is it affordable to let the application/server wait a little longer for CPU requests? Think of a mail server, for instance, where it wouldn't be a big deal if the server would forward your mail a few milliseconds later or earlier (would it?).  
  
Basically, what we need is a _load profile_ for a server. A load profile contains information like:  


  * Load during hour, day, week, month (or any other relevant period for this server)
  * Expected response times instead of observed response times (basically, a cutoff on the resources)
  * Current hardware inventory
  * Current 'scaled' hardware inventory (20% CPU usage is different for a quad core than a single core, a scaled inventory takes that into account and enables easy comparison of systems)
  * Etc.
  
  
More about load profiles later...
