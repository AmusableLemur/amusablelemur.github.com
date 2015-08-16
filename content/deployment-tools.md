---
date: "2015-01-21"
title: What deployment tools can do for you
type: post
---

I restarted work on one of my older hobby projects. Though I'm not really sure what my end goal is yet I got a vague idea of what I want to build and it's nice to have something of my own to code on.

While setting this project up I took some extra time to make sure I got deployments automated from the start. Proper configuration and use of tools saves **a lot** of time but it also takes several hours to a day or two to set up, depending on the project of course.

There is a ton of guides on the web on how to do this so I won't reiterate too much here. The project is version controlled with git which allows me to set up a repository directly on the server. In the post-receive hook I am able to add any commands necessary to properly manage the project.

As an added bonus I have fully integrated dependency management with Composer, automated asset optimization with Assetic and database migrations (that write themselves!) with Doctrine. The result is that I write some code, run a command to generate migrations if the code touches the database, and commit before pushing to live.

And that's it.

I don't have to SSH into the server to manually do a pull. There's no need to optimize and minify CSS and JavaScript on my dev machine. I don't have to worry about out of date dependencies. Heck, I don't even have to write any SQL. It just works.
