---
author: Toni
comments: true
date: 2007-12-17 16:33:00+00:00
layout: post
slug: performance-monitoring-correlations
title: 'Performance Monitoring: Correlations'
wordpress_id: 58
tags:
- Capacity
- Monitoring
- Performance
---

Although I have been arguing that performance monitoring and capacity planning require a decent server montoring environment, it also requires more. This extra part comes from the fact that often services depend on each other. A web service connects to a database (hosted on a different server) and fetches data from the file server (local, or SAN/NAS). Often, one part in the chain is a bottleneck for the whole of the process.  This is a shame and can be avoided by careful analysis of the correlations between performance data.  
  
Again, this is an argument in favor of what I called a '[load profile](http://verbeiren.blogspot.com/2007/12/performance-monitoring-more-about-peaks.html)' earlier. By _modeling_ a server by means of a load profile, we get a _representation_ of that server in terms of measurable quantities. Statistics and mathematics in general can then help us analyze the correlations between those load profiles.
