---
date: "2015-06-09"
title: How to license your software properly
type: post
---

*(Disclaimer: I am not a lawyer, everything in this post is probably wrong)*

Too many times I've stumbled across a really useful library or framework that is ridiculously prohibitively licensed. The thing is that most people are simply oblivious to what the license entails and just slap on a GPLv3 (because everyone is using GPLv2, and of course you want the latest version.. right?).

The problem with GPL is that it includes a copyleft. This means that any distributed work that uses *anything* licensed under GPL is required to be released under a GPL license as well. The reason for this is to force organizations that are developing proprietary software to release their improvements back into the wild.

This is a really good thing in most cases. The Linux kernel use this license to make sure that any company using their code is required to release any bug fixes or features free for everyone. The thing with GPLv2 is that this only applies to your *entire* project if you include GPLv2 licensed code in your project code base. If you use a third party library or module which is distinct from your code you're fine and are free to ignore the limitations of the license.

However, this was recognized by GNU and GPLv3 was soon released to fix this *"problem".*

So when you license your new awesome library under GPLv3 you are essentially forcing everyone else that use your library to also license their code under the same license. And now nobody can use your code for anything without releasing all of their own code for free.

If you want to prevent people from profiting on (and using) your code you should go ahead with a GPL license. Otherwise pick something else, I explain some of the most common licenses below. Sorted from least to most complex.

#### [WTFPL](http://www.wtfpl.net/)

This is "(Do) What The Fuck (You Want To) Public License" which is effectively the same as releasing your software under the public domain (which is useful in countries where that's not a thing). By releasing your code under WTFPL you allow people to do anything they want with it.

#### [MIT](http://opensource.org/licenses/MIT)

The MIT license was developed at MIT (duh!) and is almost the same as WTFPL except that it includes two important points. The first is that the copyright notice must remain intact, i.e. they are not allowed to remove your license from your code. Note that this is not the same as giving any notable recognition for using your code in a released product.

The second point which is far more important is that it removes any liability from using your code. If your code accidentally deletes important files or causes a company financial losses they can't claim any damages from you.

If you don't know what license to pick. Pick this one.

#### [BSD](http://opensource.org/licenses/BSD-3-Clause)

Since MIT had their own license it was only a question of time before Berkeley created one of their own as well. The BSD license is almost identical to the MIT license except for one additional point.

This license explicitly prohibits the use of your name or your organization in endorsement of the end product. Anyone using your code is not allowed to claim that you are endorsing their product by letting them use your code.

A rather important thing about the BSD license is that there are two versions. One with four clauses and one with three. The three-clause version is *the* BSD license and the one you should use if you choose to use this license.

#### [Apache License](http://opensource.org/licenses/Apache-2.0)

This is the most complex license and I admit that I don't entirely understand what all of it means. Note that the Apache license is different from Apache (which is a web server) and Apache software foundation (that are maintaining the web server and this license, among other things).

What makes Apache different from the other licenses (apart from it's far more complex legalese) is that it grants anyone using your code a patent license for any patents that cover your source code. Because copyright and patents are entirely different animals this protects the licensee from patent infringement which makes your code safer to use.

I hope that this gives some clarity in the jungle that is licensing and copyright.
