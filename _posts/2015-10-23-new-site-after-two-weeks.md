---
layout: post
title: "New site after two weeks"
description: 
headline: 
modified: 2015-10-23 10:57:03 +0200
categories:
- Website
tags: []
imagefeature: 
mathjax: 
chart: 
comments: true
featured: false
---

I've been running for about 2 weeks on Jekyll now. I spent about 2 hours during that week cleaning out some glitches and doing some more tuning.

# Permalinks

The permalinks where not as I wanted them to be, and they were not compatible with the Wordpress permalinks I used. As a consequences, internal links were not resolved correctly.

That was easily solved by using the following in `_config.yaml`:

    permalink:        "/:year/:month/:title/"

# Markdown and Rake

I improved the writing workflow as well...

First off, having posts in [Markdown](https://daringfireball.net/projects/markdown/) format is nice and doing the configuration using [YAML](https://en.wikipedia.org/wiki/YAML) is even better. Just adding an option `featured: true` in the YAML frontmatter of a post makes sure it ends up in the _Featured_ section of the site.

One slight disadvantage of the whole text-based publishing approach is the naming of the files and providing the YAML frontmatter. This is where [Rake](https://github.com/ruby/rake) comes in. Rake is similar to [GNU Make](https://www.gnu.org/software/make/). I started off with the default `Rakefile` [provided by the Notepad theme](https://github.com/hmfaysal/Notepad/blob/gh-pages/rakefile) I'm using and modified it slightly. Creating a new post is now as simple as:

    rake new['Title of the post']

Unfortanetely, that didn't work for me. Turned out, it's `zsh` being too eager interpreting what I type in the shell. This solves it:

    noglob rake new['Title of the post']

So now, I just have to open the file created by this command and write.

# Writing

I've been using [Alfred](https://www.alfredapp.com/) for a couple of years now, in the beginning just as an application launcher but slowly using more and more of its features. While writing for the blog, I especially like the search keywords. Just pressing `Alt-Space` and symple typing `google <searchterm>` brings up a chrome tab with the result of the Google search. The same can be done for Github searches, etc.

This significantly speeds up writing when adding links to pages.

# Comments

I ported the comments from the old Wordpress site to [Disqus](https://disqus.com/). I was very much impressed by the result. Just point Disqus to the Wordpress XML export file (first cleaned up by running `lint` on it) and _BOOM_. Comments added like they were before, connected to the right post.

# Local and Hithub config

For local hosting (using `Jekyll server`) and Github hosting, you need different settings for the `url` in `_config.yaml`. 

I documented this on the [Tips and Tricks page](/tricks).

