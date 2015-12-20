---
date: "2014-08-10"
title: How I set up Pelican for blogging pt. 1
type: post
---
No, this blog still uses ~~WordPress~~ (now Hugo!) because of its convenvience and ease of use. But I needed a way to document my personal server that I use for Mumble, IRC and my small projects and I decided to test out static blog generators for that.

Normally people use [Octopress][1] (based on [Jekyll][2]) which labels itself as "A blogging framework for hackers" which is cool and all but I really don't like Ruby and I had heard a lot of good stuff about [Pelican][3] so I went with that.

This post merely describes what's different in my own approach and isn't very detailed in itself, for a better tutorial in setting things up I recommend the [documentation pages][4] on how to get started.

Installing Pelican was a breeze, running `sudo pip install pelican markdown` installs both Pelican and the required packages to write in Markdown (normally you do this in a virtual environment but since I normally don't work in Python this isn't a concern for me). Following this up with `pelican-quickstart` generates a good basic template for getting started in the current directory.

I set up my blog in `~/Projects/Pelican` and instead of using the make tools included with the quickstart package I set up my own alias in `.bash_aliases` like so `echo "alias blog='pelican ~/Blog -o ~/Projects/Pelican/web -s ~/Projects/Pelican/pelicanconf.py'" >> ~/.bash_aliases`. This allows me to write my blog posts in the "Blog" folder in my home directory and then just call `blog` to re-generate the blog when I'm done.

Of course this requires me to create a virtual host in Nginx that points to the output folder, but I prefer this over running a dedicated Python server since it allows for some better caching options as well as better performance and less resource hogging on the server.

 [1]: http://octopress.org/
 [2]: http://jekyllrb.com/
 [3]: http://blog.getpelican.com/
 [4]: http://docs.getpelican.com/en/3.4.0/quickstart.html
