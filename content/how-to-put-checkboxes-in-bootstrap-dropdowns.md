---
date: "2013-07-26"
title: How to put checkboxes in Bootstrap dropdowns
type: post
---
[Bootstrap][1] is an extremely useful set of tools which, I personally believe, everyone should know about and use for their own internal projects. It's ridiculous what a time saver it is, especially combined with [Font Awesome][2] to get over 360 free, scalable icons to use with Bootstrap.

Bootstrap also have these amazing JavaScript tools which, for instance, allows you to place a dropdown menu on virtually any element. The only problem with these are that you can't really put forms in them, since the dropdown closes when you click on it. So I looked over Stack Overflow and Google and found all sorts of elaborate solutions to it, some where pretty good, others not so much.

However, they were all very involved to set up and configure, and was generally a lot more than I needed so I was hesitant to implementing them and looked a bit more until I stumbled across an [issue on GitHub][3] where someone proposed a better solution.

So I added their JavaScript and some padding, and a scrollbar through CSS for appearances and got a very simple but still solid solution to my problem. I uploaded my final result to JSFiddle (<http://jsfiddle.net/VEKYN/>). It's amazing how much time and effort you can save by just looking a little bit more at what's already available.

 [1]: http://twitter.github.io/bootstrap/
 [2]: http://fortawesome.github.io/Font-Awesome/
 [3]: https://github.com/twitter/bootstrap/issues/2097
