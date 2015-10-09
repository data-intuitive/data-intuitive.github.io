---
author: Toni
comments: true
date: 2015-01-15 21:26:35+00:00
layout: post
slug: transposing-a-spark-rdd
title: Transposing a Spark RDD
wordpress_id: 551
categories:
- Data
- Spark
---

I have been using [Spark](http://spark.apache.org/) quite a lot for the last year. At first using the [Scala](http://spark.apache.org/docs/latest/programming-guide.html#tab_scala_0) interface, but lately more using the [Python](http://spark.apache.org/docs/latest/programming-guide.html#tab_python_0) one.

In one of my recent projects, I received a dataset that contains expression profiles of chemical compounds on genes. That is to say, I got a dataset which had this data transposed, i.e., genes versus compounds, but that is not a handy format to work with. I load the original data into an RDD, but then I have to transpose this RDD.

I have been looking on the web but found no complete solution. Recently, a similar question came up on the Spark mailinglist. So I thought it is about time that I posted my approach.

This is the code for the function that transposes an RDD and returns a new RDD. There are other approaches, and there is room for optimisation as well. But this already gets the work done.

```python
def rddTranspose(rdd):
    rddT1 = rdd.zipWithIndex()
            .flatMap(lambda (x,i): [(i,j,e) for (j,e) in enumerate(x)])
    rddT2 = rddT1.map(lambda (i,j,e): (j, (i,e)))
            .groupByKey().sortByKey()
    rddT3 = rddT2.map(lambda (i, x): sorted(list(x), 
                        cmp=lambda (i1,e1),(i2,e2) : cmp(i1, i2)))
    rddT4 = rddT3.map(lambda x: map(lambda (i, y): y , x))
    return rddT4.map(lambda x: np.asarray(x))
```

This code converts the rows to numpy arrays in the return statement, so you need to import numpy as np. This step is strictly speaking not necessary, but it does make subsequent random access _inside_ the rows faster. It must be noted as well that the procedure only works when one row (one element of the original RDD as well as the transposed RDD) fits into the JVM memory of the workers.

I left out the comments in my code, to keep it a little exciting for you...
