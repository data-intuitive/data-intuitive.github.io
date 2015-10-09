---
author: Toni
comments: true
date: 2013-08-16 12:48:26+00:00
layout: post
slug: turning-cloudera-quickstart-vm-into-an-r-studio-server
title: Turning Cloudera Quickstart VM into an R Studio Server
wordpress_id: 461
---

Downloading the image (in my case for VirtualBox) is easy enough. Make sure that the VM has a connection to the internet.

    
    sudo yum -y install R
    sudo yum -y install wget




From the [R Studio Server website](http://www.rstudio.com/ide/download/server):

    
    wget http://download2.rstudio.org/rstudio-server-0.97.551-x86_64.rpm
    sudo yum install --nogpgcheck rstudio-server-0.97.551-x86_64.rpm




Ready! Make sure to connect using a local user (if necessary, create one).

There's one caveat though. R version 3.0.1 is installed and most packages for working with Hadoop are not yet ported to version 3.

A quick workaround is the following:

Within R:

    
    install.packages(c('Rcpp','RJSONIO','bitops','digest','functional','stringr','plyr','reshape2','rJava'))




From the console:

    
    wget https://github.com/RevolutionAnalytics/rmr2/raw/master/build/rmr2_2.2.2.tar.gz



    
    wget https://github.com/RevolutionAnalytics/rhdfs/raw/master/build/rhdfs_1.0.6.tar.gz



    
    wget https://github.com/RevolutionAnalytics/rhbase/raw/master/build/rhbase_1.2.0.tar.gz




From the console:

    
    sudo R CMD INSTALL r*.tar.gz




This should do the trick!


