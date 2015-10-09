---
author: Toni
comments: true
date: 2013-11-25 14:20:40+00:00
layout: post
slug: running-docker-on-macosx
title: Running Docker on MacOSX
wordpress_id: 490
---

I found out about [docker](http://www.docker.io/) this morning via [the blog of the people behind AMPlab](https://amplab.cs.berkeley.edu/2013/10/23/got-a-minute-spin-up-a-spark-cluster-on-your-laptop-with-docker/), creators of Spark and such. In short (because it's actually much more than this) it lets you run a Spark/Shark cluster (pre-built!) on your PC.

I want to use it to experiment with a (virtual) Spark/Shark cluster on my laptop. Isn't that cool?!

Unfortunately, docker is built for Ubuntu. Fortunately, there are instructions on how to set it up on other systems.

Two things needed to be done before I got it to work:



	
  1. Upgrade the amount of memory available to Vagrant to 2GB. See here: [http://docs-v1.vagrantup.com/v1/docs/config/vm/customize.html](http://docs-v1.vagrantup.com/v1/docs/config/vm/customize.html).

	
  2. Edit the [nameserver script](https://github.com/amplab/docker-scripts/blob/master/deploy/start_nameserver.sh) in order for the nameserver test to complete with success.


For the second, I changed

    
    dig nameserver @${NAMESERVER_IP} | grep ANSWER -A1 | grep 127.0.0.1 > /dev/null;


into

    
    dig nameserver @${NAMESERVER_IP} | grep ANSWER -A1 | grep ${NAMESERVER_IP} > /dev/null;
