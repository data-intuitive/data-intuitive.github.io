---
author: Toni
comments: true
date: 2013-01-18 09:59:18+00:00
layout: post
slug: slm-issues-with-traditional-slm-part-4
title: 'SLM: Issues with traditional SLM (Part 4)'
wordpress_id: 406
categories:
- Data
- SLM
---

Consider the following (fake) recommendation for a hotel room:


<blockquote>The guaranteed average room temperature is 20 degrees Celcius.</blockquote>


Even with a money back guarantee, I would not rent the room. Suppose its 40 degrees during the day and 0 degrees during the night? The average temperature may still be 20 degrees...


### Averages


When dealing with customer interactions (calls), IT incidents and problems, etc., one usually deals with a large number of instances that are observed. Hundreds or even thousands of calls may be logged in a call center per day. In order to aggregate the information on these calls, one usually takes averages over a given period of time. This is reflected in the examples given before.

Averages, however, are only a first order representation of a set of instances. One bad instance can easily be compensated by a good instance resulting in a good average. In other words, if the average on-hold time for a callcenter is 2 minutes, it may well be that I have to wait 10 minutes. If only at another time 5 calls are answered within a second, the average is back to 2 minutes.
