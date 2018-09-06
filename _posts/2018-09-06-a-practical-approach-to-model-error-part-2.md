---
layout: post
title: "A Practical Approach to Model Error - Part 2"
description: 
headline: 
date: 2018-09-06 12:00:00 +0200
categories:
- data science
- web
- math
- visualization
- model error
- fat tails
tags: []
imagefeature:
mathjax: 
chart: 
comments: true
featured: true
---

It's been a while since I [first wrote about tackling model error using a
simple model](http://www.data-intuitive.com/2016/05/a-practical-approach-to-model-error/). It's about time to come back to it.

What triggered the current post is the opportunity I was given to give a
masterclass in the [Evidence and policy summer school](https://ec.europa.eu/jrc/en/event/workshop/evidence-and-policy-summer-school-science-policy-and-demography). Since my masterclass is about uncertainty in decision making, it seemed like a nice opportunity to look back at the simple model.

# Introduction

I'm not going to introduce the model again, but I do want to reiterate that it's a very simplistic model when it comes to actually modelling the spreading of a real virus. On the other hand though, if [Nobel prizes](https://www.nobelprize.org/prizes/economics/1997/press-release/) are awarded for applying this kind of model there must be some value in it.

# Running the Different Scenarios

For the summerschool, I developed a little web application called [Incertae](/incertae/) and which allows you to run the scenarios from a browser. Just [try it](/incertae/) for yourself!

In order to make sense of the scenarios, let's walk through this step by step...

## Step 1: No Randomness

By clicking on the parameters of the simulation, or below in the footer on the words _can be changed_, the simulation settings can be adjusted.

Set the variables such that there is no randomness applied to the scenario. Only one scenario is sufficient in this case:

![](/images/incertae-step1-settings-small.png)

And see what the result looks like:

![](/images/incertae-step1-result-small.png)

## Step 2: A bit of Randomness

In step 2, we add a bit of randomness. For this we use the default settings, although you could increase the number of scenarios if you wanted to:

![](/images/incertae-step2-settings-small.png)

The result should look similar to the following. Please note that randomness has been added, so your result should not look exactly like the one presented here!

![](/images/incertae-step2-result-small.png)

## Step 3: A bit more Randomness

In step 3, we increase the amount of randomness added to the scenarios. For instance:

![](/images/incertae-step3-settings-small.png)

Now, given more randomness in the scenarios, yours might be completely different from the one below:

![](/images/incertae-step3-result-small.png)

# Discussion

To be continued
