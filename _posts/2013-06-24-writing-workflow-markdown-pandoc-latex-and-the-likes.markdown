---
author: Toni
comments: true
date: 2013-06-24 13:10:00+00:00
layout: post
slug: writing-workflow-markdown-pandoc-latex-and-the-likes
title: 'Writing workflow: Markdown, Pandoc, LaTeX and the likes'
wordpress_id: 452
---

You wouldn't tell from the updates on this website, but I'm actively writing again. Offline, that is, the online part is for later. For now, I want to share my experience improving my writing workflow.

In the past, I used [LaTeX](http://www.latex-project.org/) for scientific texts and MS Word for everything else. LaTeX gives me the professional and typographically correct texts that I want, but I spent too much time fiddling around with packages, remembering markup, etc. MS Word, on the other hand, quickly made me get things done, albeit without the professional look or scientific powers.

I'm now in a situation that any writing (technical, scientific and even prose) can be done in the same way, delivering results in PDF, html or even MS Word:



	
  1. It usually starts in [iA Writer](http://www.iawriter.com/mac/) (on the Mac or the iPad), but any word processor able to handle ASCII text can be used. I choose iA Writer because of its distraction free writing.

	
  2. [Markdown](http://daringfireball.net/projects/markdown/) is used as markup specification (including figures, footnotes, emphasis, etc.). Markdown is very basic, but it lets you focus on the content, rather than the form.

	
  3. [Programming](http://www.rstudio.com/ide/docs/r_markdown) code ([R](http://www.r-project.org/) for instance), [formulas](http://www.rstudio.com/ide/docs/authoring/using_markdown_equations), etc. can all be included in the Markdown format by means of the proper notation and possibly some extensions to the parser (see step 4).

	
  4. By means of [Pandoc](http://johnmacfarlane.net/pandoc/README.html), the text is converted into the appropriate format (html, pdf, LaTeX, ePub, DocBook, ...)

	
  5. Ready!


Ok, I hear you thinking, but you just lost all possible configuration of look and feel, layout, etc... That's correct, there are some Markdown writing tools that allow you to create PDFs that look awful.

The nice thing about Pandoc though is that during the conversion step (4), you can specify the templates (CSS, LaTeX header code, MS Word template) that should be used.

It takes some fiddling in order to get the correct options to Pandoc and get proper templates in place. A Google should get you going.

An example. From a slight adaptation of this file, we generate a Markdown file and this is converted in the [PDF linked here](http://www.data-intuitive.com/?attachment_id=453). A similar process is used to create the reports for the different analysis steps for the [dataMineR project](https://github.com/tverbeiren/dataMineR).

Leave a comment if you would like to see more examples.


