---
author: Toni
comments: true
date: 2007-10-26 08:00:00+00:00
layout: post
slug: vmware-capacity-planner-taking-the-data-offline-part-2-cygwin-wget
title: 'VMware Capacity Planner: taking the data offline (Part 2: Cygwin & wget)'
wordpress_id: 52
tags:
- Capacity
- Monitoring
- Performance
- Virtualization
- VMware
---

I started thinking about avoiding [the manual exports](http://verbeiren.blogspot.com/2007/09/vmware-capacity-planner-taking-data.html) from the VMCP website and remembered I used [WGET](http://www.gnu.org/software/wget/) in the past for this kind of stuff. The difference with before was that this time, I needed to login to the website before being able to get data from it.  
  
Login in to the VMCP [website](https://optimize.vmware.com) is done using a POST method and luckily wget supports that.  The next thing is to understand what the post data needs to be.  This can be fetched from the source of the logon page:  
[![](http://bp1.blogger.com/_BQpPXr1uJkU/RyGsu5e3vzI/AAAAAAAABI0/NO6_D9Brfqo/s320/logon.jpg)](http://bp1.blogger.com/_BQpPXr1uJkU/RyGsu5e3vzI/AAAAAAAABI0/NO6_D9Brfqo/s1600-h/logon.jpg)  
  
The relevant POST data is derived to be  
`  
fuseaction=Security  
Page=users_login.cfm  
username=???  
password=???  
`  
  
Since I run Windows XP on my laptop, I use [Cygwin](http://www.cygwin.com/) to run wget.  Cookies are used to store a session ID for you logon session, so wget has to be told to store those cookies in a file. This is the resulting command line:  
  
`  
wget --keep-session-cookies --save-cookies cookies.txt 'https://optimize.vmware.com/index.cfm' --post-data 'fuseaction=Security&Page;=users_login.cfm&username;=???&password;=???' --no-check-certificate -O output.html  
`  
  
Parsing the output.html file, you should be able to see whether logon was succesful. The success depends on many factors (local proxy, network settings, username/password, etc.). You can get more info by adding suitable options to wget.  
  
This concludes part 2 of this series of articles. In this part, we used wget to logon to the VMware capacity planner website.
