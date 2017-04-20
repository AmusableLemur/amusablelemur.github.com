---
date: "2012-11-19"
title: How to combine multiple commits into one
type: post
---
If you're using Git you know how powerful it is as a CVS tool. But when Git is used as a deployment tool to be able to quickly revert changes if needed it may cause some headaches when deploying major features. There's a trade off between having one giant commit and working with Git the preferred way of using small, incremental commits when deploying in this way. If there's a critical problem with the new feature it will need to be reverted quickly which could become quite annoying if there are a lot of commits. While on the other hand it more or less defeats the purpose of using a CVS if you're never working with your history, so to solve that I present the wonderful part of Git that is known as rebasing.

By enabling Git's interactive mode with `git rebase -i [commit]` we can interactively specify what we want to do with each commit. `[commit]` should be which commit you wish to rebase *to*, that is to say, the specified commit will not be included in the rebase. You can also specify how many commits from HEAD you wish by instead of inputting the hash, subtracting the number of commits you want from HEAD with a tilde like so `HEAD~5`.

This should open up your text editor with the list of commits you've chosen and their messages.

    pick b386745 Backed changes as they broke the autoloader
    pick 385d14b Added precautions to model
    pick 96aec4c Updated datamapper
    pick 77fc647 Added isset to models
    pick 7ac5e2d Added newline to main controller
    pick 1a0a08b Cosmetic updates
    pick 7a35bfa Re-added file_exists()
    pick 2e98b00 Added ordering to database abstraction layer

As you should see, they're sorted in reverse chronological order. *Pick* means that it should use the commit, if you let the first commit stay as *pick* and change the others to *squash* all the other commits will be joined into the first one. After this you need to write a new commit message for the new squashed commit which defaults to all the previous messages after each other and then you're done!
