---
author: Toni
comments: true
date: 2013-01-21 06:00:47+00:00
layout: post
slug: slm-issues-with-traditional-slm-part-5
title: 'SLM: Issues with traditional SLM (Part 5)'
wordpress_id: 410
categories:
- Data
- SLM
---

### Focus on the wrong instances


A consequence of dealing with averages and aggregate metrics is that in some cases, when a threshold value is reached there is no longer an incentive to act on the individual instance that went wrong. As an example, consider example 6 [given before](http://www.data-intuitive.com/2012/11/slm-introduction-part-1/). If the resolution time of an incident is above threshold, it is counted in the percentage and it will not get any better over time, but also not worse! In other words, there is no longer a reason to fix the incident as soon as possible. Rather, it may be better to focus on other incidents that can still be fixed within threshold.

The result may be a large number of open incidents and thus unhappy customers, and rightly so.


