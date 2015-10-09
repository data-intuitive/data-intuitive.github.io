---
author: Toni
comments: true
date: 2014-07-10 10:14:43+00:00
layout: post
slug: publishing-html-presentations-on-github
title: Publishing html presentations on Github
wordpress_id: 503
categories:
- Data
- Writing
---

You've seen those [fancy html presentations](https://github.com/hakimel/reveal.js/wiki/Example-Presentations) on the web? [Reveal.js](http://lab.hakim.se/reveal-js) is a framework to create such things of beauty. And it goes along well with my [Markdown](http://www.data-intuitive.com/2013/06/writing-workflow-markdown-pandoc-latex-and-the-likes/) based style of writing, even for presentation slides.

I usually create the presentations on my laptop, using [Pandoc](http://johnmacfarlane.net/pandoc/) to convert to html. In principle, this should be ready for the web by default. If only I had an easy hosting solution to move it to.

[Github](https://github.com/) allows you to host html files and even complete web sites. I had never tried it myself, but now I did. It's really simple. Move your repository into the branch `gh-pages` (you can do this on the Github website) and finished. The web site is accessible via `http://<username>.github.io/<projectname>`. This is what Github calls a _Project Page_.

Behind the scenes, Github uses [Jekyll](http://jekyllrb.com/) for building static website from source files in, e.g., Markdown format. When you publish something to the `gh-pages` branch, it automatically kicks in... and gave very vague errors in my case.

After some trial and error, I found out, the best approach is to install `jekyll` yourself and launch it locally. This immediately gives a readable error message. It turned out I had a stale symlink in my directory tree. Removing this removed the building issue for Github.

The result can be seen here: [http://tverbeiren.github.io/BigDataBe-Spark](http://tverbeiren.github.io/BigDataBe-Spark).

BTW, in order to install `jekyll` on my MacBook Air, I had to install a newer version of `Ruby` (tip: use `rvm` for this, [link](https://rvm.io/)).
