---
date: "2014-01-13"
title: Fucking sudo
type: post
---

I stumbled across [this comment][1] a while ago and though it was pretty funny, so I wrote a basic one liner to add the "feature" to my shell. Basically what it does is allowing you to write "fucking" instead of "sudo" for the humorous effect of it, example below.

    $ make install  
    No.  
    $ fucking make install

Here's the code for setting it up. The specified configuration file needs to be changed for it to work in other shells than bash.

    $ echo "alias fucking='sudo'" >> ~/.bashrc && . ~/.bashrc

 [1]: http://www.reddit.com/r/programming/comments/1sqnj7/416d65726963612043616e20436f646520/ce0jnoq
