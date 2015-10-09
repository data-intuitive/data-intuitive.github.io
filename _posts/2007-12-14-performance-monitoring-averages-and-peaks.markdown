---
author: Toni
comments: true
date: 2007-12-14 16:22:00+00:00
layout: post
slug: performance-monitoring-averages-and-peaks
title: 'Performance Monitoring: Averages and Peaks'
wordpress_id: 56
tags:
- Capacity
- Monitoring
- Performance
---

Now that we are into the topic of performance (of capacity) monitoring and planning, let us continue with something that has kept me busy the last couple of days: averages of performance data (and other statistical information) versus peaks.  
  
This goes back to a classic textbook example in statistics, where the mean value of a series of data points is completely irrelevant as a representation of the data points itself. Let us consider the following example.  Given a series of data like in the table below:  


<blockquote>  
  X     Y  
  A     1  
  B     2  
  C     4  
  D     7  
  E     100  
  F     4  
  G     9  
  H     7  
  I     3  
  J     5  
</blockquote>

  
These may, for instance, represent scores (0-100) given to students (by a very strange teacher).  In a graph, this is presented below:  
  
[![](http://bp1.blogger.com/_BQpPXr1uJkU/R2KgD3gKdLI/AAAAAAAABXk/m_ET5w6qC1w/s320/Table-data.jpg)](http://bp1.blogger.com/_BQpPXr1uJkU/R2KgD3gKdLI/AAAAAAAABXk/m_ET5w6qC1w/s1600-h/Table-data.jpg)  
  
The red line represents the average value. It is clear that everyone (except the teacher's little friend with 100 points) is below the average. As a consequence, the average is not a good representation of the data as a whole. Some say it is too much influenced by the extreme values. In fact, this average (sum of the data values divided by the total amount of data points) is called the arithmetic mean. There is another notion of 'an average' which is called 'geometric mean'. In the example above, the value of it would be 5.4 which is much more relevant. The median would even better define the data set, but that would lead us too far.  
  
Basically, the fact that the arithmetic mean does not give a good indication of the data set is caused by the large spread of the data. In statistics, there is another indicator for this: the variance, or standard deviation. It is a measure for how close or far apart the values are.  In the example above, the standard deviation. In our example above, it would read 30.2. Suppose the value of E would be 10 instead of 100, the standard deviation becomes 3. In others words, the lower is the standard deviation, the more the data is 'close'.  
  
The above brings me back to performance monitoring. Somehow, I want to summarize the performance data of a server by a small set of indicators (averages of time etc.) that give a reasonable picture of the actual performance or in other words: that are representable for the system's actual performance. Typically, when looking at the percentage a CPU is used over time, we see fluctuations that are similar to the figure above (don't believe me, below is an actual example of a system with some high peaks and further sitting idle for most of the time - this server has 4 cores by the way). We conclude that, therefore, it does not make much sense to look at simple averages of the performance counters in order to get an idea of the behavior of the system..  
  
[![](http://bp1.blogger.com/_BQpPXr1uJkU/R2KgS3gKdMI/AAAAAAAABXs/tnoBw8RDtlA/s320/CPU-fluctuations.jpg)](http://bp1.blogger.com/_BQpPXr1uJkU/R2KgS3gKdMI/AAAAAAAABXs/tnoBw8RDtlA/s1600-h/CPU-fluctuations.jpg)  
  
Coming back to VMware Capacity Planner: the tool keeps track of the average value (yes, the simple average that does not say much) but also internally uses the geometric mean but not the variance (as far as I can tell). From this perspective, the whole performance gathering using this tool would be worthless. Luckily, it also keeps track of peak values (and calculates averages over these peaks but that is another story). Comparing the peak values with the average tells us a lot about the spread of the data points. The system behind the graph above, has an average CPU value of less than 20% while the peak CPU utilization is higher than 90%! This tells us that the variance/spreading in data points is large.  
  
In a virtualization/consolidation assessment, these cases have to be taken into account, as we do not want our systems to become unresponsive because they have their peaks at the same time. More about this and other topics later...
