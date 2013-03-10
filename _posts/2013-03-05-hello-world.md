---
layout: post
title: "Hello, world"
description: "The first post in my new blog."
category: 
tags: []
---
{% include JB/setup %}

Hello there. It's probably about time I created a public blog (I'm not counting the one I had somewhere on a free geocities-style host back in 2002). This will hopefully be a place for me to dump thoughts and notes about things, most likely to be related to software development. 

At the moment, the blog is just a static site hosted on [Github Pages](http://pages.github.com), hastily cobbled together with a useful tool called [Jekyll-Bootstrap](http://jekyllbootstrap.com) which quickly and easily generates a skeleton site for preprocessing with [Jekyll](https://github.com/mojombo/jekyll).

As I wanted to get this blog up and running with minimal time and cost effort, I wanted to avoid using a CMS such as Wordpress and liked the idea of generating the site from markdown content parsed through Jekyll. I considered using Amazon S3 to host the static site once pages were created but given that this would cost money and require at least one more step than pushing the content to a git repo, I decided to go with Github Pages. Currently the deployment process is: generate post template for blog post -> type content into file -> push to Github, which is extremely simple!
