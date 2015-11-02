---
layout: post
title: "Thoughts on the Spark Summit Europe 2015"
description: 
headline: 
date: 2015-10-29 19:09:01 +0100
categories:
- spark
- distributed computing
- data science
tags: []
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---


In this post, I summarize some of the things I picked up at the Spark Summit. Some of these require more thought or research, but at least I'll have a to do list of things to look back at.

In the meanwhile, a lot of the [talks are posted already on Youtube](https://www.youtube.com/channel/UCRzsq7k4-kT-h3TDUBQ82-w).

So, let's get started.

# Dataframes

I've been putting off using dataframes for a year now. There are two main reasons for doing this:

1. I like the (functional) API of the `RDD`'s more than the dataframes API.
2. I can do more with the `RDD` API which I need for most of the applications we're working on.

Unfortunately, a lot of the cool work on Spark and especially the machine learning (ML) and optimization (Tungsten) work is currently focussed on dataframes. I understand that, multiple people have explained why that is, but still I keep on thinking about the two reasons above.

In the next release (1.6), a new API will be available: [__DataSets__](https://twitter.com/setema/status/659288204470808577). And it is exactly what I need to be happy using dataframes: The dataframe API, extended such that you can use the traditional functional API as well.

# sparkR

For the same reason I hadn't used dataframes yet, I have not yet tried out using sparkR: it uses dataframes. The limitations of the dataframe means that when it comes to transforming the data in a dataframe, you are limited to the functions that are provided.

In Scala, it's possible to define a UDF (User Defined Function), but until now that was not possible in sparkR. The next version of Spark, however, should support just that.

# Databricks Cloud

I've been really impressed by the Databricks notebooks. Having worked with different Open Source notebooks already (iPython, Zeppelin, Spark-Notebook), this one is definitely better.

Some highlights:

- Very intuitive interface and extremely easy to attach a cluster to a notebook
- Multiple users on the same notebook works seamlessly, and much like editing a Google Document
- Good revision history
- Import code from files (`%run ...`) or from [Github](http://www.github.com)
- Included REST Server
- Interoperability between different notebooks

# Spark Streaming

Spark streaming has long been the part of the Spark package that was least covered and used. Everyone found it cool and interesting.

Now, during the talks, it became clear that the streaming aspect of Spark is very important. Lot's of use cases described how they use Spark Streaming in their application, even in production.

# ML pipelines

I [read about it](https://databricks.com/blog/2015/01/07/ml-pipelines-a-new-high-level-api-for-mllib.html). It looked cool on paper. Turns out it is even better in practice.

Many times, different steps occur when going from a dataset to a model and predictions. Often-times these steps are poorly documented and as a consequence not reproducible.

Now, with pipelines, you get a high-level API for configuring and running the different stages of a process. Downside is that it is yet another API to learn. But in this business, we don't mind learning a few APIs...

It becomes even more interesting when the set of underlying algorithms and methods gets extended: hyper-parameter tuning, ML models, ...







