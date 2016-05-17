---
author: Toni
comments: true
date: 2015-05-29 13:45:42+00:00
layout: post
slug: code-snippet-repository
title: Code Snippet Repository
wordpress_id: 559
categories:
- Scala
- Spark
- S3
- Code
tags: []
imagefeature: 
mathjax: flase
chart: 
comments: true
featured: false
---

I'm jumping between Scala/[Spark](http://spark.apache.org/) coding, some Javascript in between, Python/PySpark and then some [R](http://www.r-project.org/) every now and then. This in itself is already a challenge, but the worst thing is that I frequently encounter situations where I think: _I've encountered this situation before_. In many cases, it's a situation that required quite some work to resolve. You end up with two possibilities: 1) retrieve the solution from some code somewhere on your harddisk or 2) start finding the solution again from <del>scratch</del>Google.

So I'm now wondering if this could not be organized better... Of course it can, but how? [Github](https://gist.github.com/) has the ability to store snippets of code, I could just keep a file handy for every programming environment/language. What are you using?

Here's an example of a snippet of Scala code that I need a lot: configuring a Spark context to use my credentials (store in environment variable) to connect to [Amazon S3](http://aws.amazon.com/s3/):

```scala
val fs_s3_awsAccessKeyId = sys.env.get("AWS_ACCESS_KEY_ID").getOrElse("<key")
val fs_s3_awsSecretAccessKey = sys.env.get("AWS_SECRET_ACCESS_KEY").getOrElse("<key>")
sc.hadoopConfiguration.set("fs.s3n.awsAccessKeyId", fs_s3_awsAccessKeyId)
sc.hadoopConfiguration.set("fs.s3n.awsSecretAccessKey", fs_s3_awsSecretAccessKey)
```

How do you cope with this challenge?


