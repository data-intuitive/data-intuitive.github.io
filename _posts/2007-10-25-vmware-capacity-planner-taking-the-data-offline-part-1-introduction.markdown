---
author: Toni
comments: true
date: 2007-10-25 07:00:00+00:00
layout: post
slug: vmware-capacity-planner-taking-the-data-offline-part-1-introduction
title: 'VMware Capacity Planner: taking the data offline (Part 1: Introduction)'
wordpress_id: 51
tags:
- Capacity
- Monitoring
- Performance
- Virtualization
- VMware
---

Lately, I have been involved in some VMware Capacity Planner (VMCP) tracks. VMCP deals with monitoring a set of (physical) servers in order to assess possible virtualization scenarios.    
  
VMCP works in the following way: a monitoring server is set-up with a tool that does (but is not limited to) regular performance measurements. This tools sends the data to a VMware database through the web (over a secure channel). Via [a web interface](https://optimize.vmware.com), one can then query the information, get reports, view trends, show graphs, configure and create consolidation scenarios, etc.  Usually, we let the system run for around 4 weeks to get a realistic idea of the performance characteristics.  
  
What I like about VMCP is that the data is not located at the customer site, and available at all times (once it has been uploaded). This gives me the opportunity to regularly check on the status of the performance measurements.   
  
The biggest disadvantage of VMCP is that the web interface is not the most flexible and fast interface around. Some things I would like to do are not available (lack of flexibility) but could easily be done in, e.g., Excel and at times when everyone in the world is awake it takes ages to refresh a page and get the result of a query. Moreover, it is not easy to get good-looking information to paste in a document.  
  
When it comes to writing a report, the customer is obviously not only interested in a statement like: you will need 5 ESX server of type X to cope with the load. Therefore, I like to add tables with the most useful metrics (CPU, network, Disk I/O, ...) for later reference. I add this information as an appendix.   
  
This is where I would spend at least half a day exporting CSV files from the VMCP website, loading them in Excel, laying it out as a nice table and paste it in the document. I started thinking about automating some of the steps required, and I covered the most time-consuming already: exporting the information from the website as a CSV file.  
  
In the following part, I'll explain how I started this little adventure...
