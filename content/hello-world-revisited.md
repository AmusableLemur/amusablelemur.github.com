+++
title = "Hello world revisited"
date = "2015-07-26T10:11:46+02:00"
type = "post"
+++

So I finally made the jump to a static blog.

I have been contemplating this move for quite some time now. Mostly it's been a
consideration between [Pelican](http://blog.getpelican.com/) (Python) and
[Jekyll](http://jekyllrb.com/) (Ruby). Where Jekyll has been more tempting with
the huge ecosystem around [Octopress](http://octopress.org/) to benefit from.

The downside with Jekyll, and Octopress especially, is that I have to keep an
entire framework of blog generating software around. This was a lesser problem
with Pelican which was smaller, but still a limitation.

Enter [Hugo](http://gohugo.io/). Hugo is (yet) another static blog generator,
this time written in Go. While I don't have to touch any of the Go code myself
it has some benefits in being compiled and because of that it's blazingly fast.
It also doesn't enforce any directory structure or configuration formats (the
default being TOML).

Setting everything up has been a breeze. I write my posts in Markdown, commit
them to a GitHub repository which automatically notifies a build system which
downloads everything and generates the blog. It then uploads the generated blog
files to the web server and \*bam\*, we're live.

I will keep this blog on a temporary domain until I have managed to migrate over
all my old posts. Or well, at least the ones I'd like to keep.

Update: I have finally begun migrating my old posts so this blog has replaced my
old one. A lot of old content has disappeared in the migration. I've kept what
little I liked as well as the posts that got a lot of traffic.
