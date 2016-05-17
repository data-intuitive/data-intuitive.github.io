---
author: Toni
comments: true
date: 2014-09-24 05:00:52+00:00
layout: post
slug: writing-workflow-and-reproducible-data-analysis
title: Writing Workflow and Reproducible Data Analysis
featured: true
categories:
- Writing
- Workflow
- Reproducible Data Analysis
---

I've been writing about my [writing](http://www.data-intuitive.com/2013/06/writing-workflow-markdown-pandoc-latex-and-the-likes/) [workflow](http://www.data-intuitive.com/2013/10/activity-monitoring-from-smartphone-sensor-data-in-a-new-layout/) [before](http://www.data-intuitive.com/2014/07/publishing-html-presentations-on-github/). Since some aspects of it are related to reproducible research and especially reproducible data analysis, I have [collected some material and tips](https://github.com/tverbeiren/ReproducibleDataAnalysis) in a presentation I gave last week on my [Github](https://github.com/tverbeiren):

[![RR](/images/RR.png)](https://github.com/tverbeiren/ReproducibleDataAnalysis)

One aspect that I did not yet mention there, is how I approach this on my Mac. This depends a little bit on what type of text I'm writing. Data analysis is usually done within [RStudio](http://www.rstudio.com/). It has very good functionality for generating PDFs and the like, but I still prefer my own Makefile and knitr/Pandoc combination.

Less technical texts are usually writing using i[AWriter](http://www.iawriter.com/mac/), but sometimes also in [Sublime Text](http://www.sublimetext.com/). iAWriter by default has support for Markdown, Sublime Text can be configured with a very good Markdown plugin. I use [Marked](http://marked2app.com/) for previewing, proof-reading, etc.

Drop a comment if you want more info, or have a tip to share yourself.
