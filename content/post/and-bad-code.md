---
date: "2021-08-15"
title: If you are using "and" you are writing bad code
type: post
---

Mostly everyone would agree that blindly writing SOLID code just for the sake of it does more harm than good. Just look at any example of the "enterprise editions" for [FizzBuzz](https://github.com/EnterpriseQualityCoding/FizzBuzzEnterpriseEdition) or [Hello World](https://gist.github.com/lolzballs/2152bc0f31ee0286b722). This is not to say that SOLID, KISS, DRY and so on are not useful guidelines for improving code quality and general practice. The practice that best aligns with the project goals is pretty much always the best option.

Regardless of some peoples opinion of SOLID as a whole I think that most would agree with me that the single responsibility principle is fantastic. Making sure that a function (or method) only does the one thing it describes, i.e. ideally without side effects, and that a class (or file, or package) only has one responsibility makes for cleaner code that is easier to understand.

This is also true for version control with commits and pull requests. For example, if your commit message includes the word "and" it should be two commits. If your documentation describes a method using the word "and" it should probably be split up into two or more smaller methods.

Stretching this a bit to include overgeneralized descriptions is helpful as well. Putting stuff in a folder called "extra" or in a module called "util" follows the same principle as using the word "and". It should probably be split up and put elsewhere.