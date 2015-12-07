---
layout: default
---

## Bash

Delete files from a certain age

```bash
find . -mtime +20 -type f -delete
```

When directories _and_ files need to be deleted, use this instead:

```bash
find . -mtime +20 -type d -type f -delete
```

This in fact means putting AND between the two types. The following is _better_:

```bash
find . -mtime +20 -type d -o -type f -delete
```


## Jekyll

Testing a Jekyll site locally and making it available via Github by pushing it to the git repo _without_ making any configuration changes is a pleasure. But it's not very easy to do that. I found the following trick to work very well.

Make two config files, one global one (which works for Github pages) and one which overrides the appropriate settings for a local deploy.

I have the following files: `_config.yaml` and `_config_local.yaml`. In `config.yaml`, I have the following line:

    url:                  'http://www.data-intuitive.com'

In `_config_local.yaml`, this setting is overriden:

    url:    'http://localhost:4000'

Locally, Jekyll can then be started like this:

    jekyll serve -w --config _config.yaml,_config_local.yaml


## Spark Notebook

Starting Spark-Notebook requires to use the host stack (for now?!). This is a working config on the cluster we use:

```
docker run -d --net=host -v /data/toniv/spark-notebook-0.6.1/notebooks:/opt/docker/notebooks andypetrella/spark-notebook:0.6.2-SNAPSHOT-scala-2.10.4-spark-1.4.1-hadoop-2.2.0-with-hive-with-parquet
```

Using files stored on `HDFS` can be done like this:

    val covFile = sc.textFile("hdfs://ly-1-09.exascience.org:54310/data/toniv/sample-1.coverage")


## Connect to running Docker instance

Use this to connect a terminal to running container for inspection:

    docker exec -it [containerID] bash



