---
date: "2022-11-17"
title: Implicit frameworks
type: post
---

These are some thoughts based on ["Using a Framework will harm the maintenance of your software"](https://berk.es/2022/09/06/frameworks-harm-maintenance/) and the discussions from the related [Hacker News thread](https://news.ycombinator.com/item?id=33185010). One of the [top responses](https://news.ycombinator.com/item?id=33185383) included the following quote which summarizes an important point neatly.

>Every sufficiently complex framework-free application contains an ad hoc, informally-specified, bug-ridden, slow implementation of half of a framework.

That even when a framework has been explicitly avoided, or a minimalistic framework used, an implicit framework will eventually develop based on the culture around the codebase. There is a "way of doing things" that emerge in any company culture which becomes the framework. This might not be a heavy ORM, forced MVC structure, OOP principles or some other scary three letter acronym. But instead of over-generalized solutions of "one size fits all" it will be a series of undocumented and glued together ad-hoc solutions created to solve one specific problem at a time.

One way of avoiding this is to just accept that a framework will eventually be necessary as the codebase, and the number of involved people, grows. But this way of commiting to using or building a framework forces a decision early which can be a daunting commitment and is often avoided in an attempt to show fast and early progress. One of the worst examples of this is an old colleague who wanted to learn exactly how [Doctrine](https://www.doctrine-project.org/) worked so that he could build his own ORM implementation.

But why do people do this, just so they can show how much valuable code they have written instead of reading boring tutorials and documentation? I think, as the article mentions as well, that people are afraid of maintenance. People are afraid of having to change version numbers in their dependency files and deal with deprecation warnings as well as upgrading from insecure versions. As if only software not invented here has bugs. The only real difference is that software used by others are tested and patched by others. Most of the time "others" means better qualified, more experienced, and more numerous people than what your own company has.

If you build it yourself you are also forced to maintain and secure it yourself. And this does not mean updating dependencies and changing version numbers. This means doing your own pentesting and patching your own code since you can no longer rely on someone elses best practices to solve your problems for you.

As a rule of thumb the best code is always no code. No code is bug-free, no code is without maintenance, and so on.

Reducing the amount of code that need to be written is almost always the ideal scenario. Using code that is written and battle tested by thousands of other people at least minimizes the amount of code you need to write yourself. This also goes for structure, design patterns, and other best practices.

With all of this said I still think that every developer should try to build a somewhat complex system without too much assistance from libraries and frameworks at least once. If only to understand how much we have available for free.
