---
date: "2016-01-17"
title: Authenticating ejabberd users with Symfony2 and FOSUserBundle
type: post
---

I've been trying to set up an XMPP server since MSN went out of style (i.e. since forever). However, managing users is a bit of a hassle and normally the two alternatives are to either create users manually or allow them to register through the client. The first is tedious and the second is not very user-friendly.

But with ejabberd there's also support for MySQL databases. Which means that I can write a simple registration service where users can manage their accounts themselves. All it takes is updating their information in the database. The downside is that ejabberd only supports plaintext password storage on external database connections which is insanely unsafe for numerous reasons.

There is an alternative though. There is an old and barely documented configuration option in ejabberd which supports external authentication. Though the documentation is lacking there exists a number of example implementations to learn from.

The configuration allows to load a separate program which ejabberd can pipe authentication data into in order to learn if the user should be able to log in or not. You can even return true for all cases in order to allow people to log in with whatever username and password they want.

Basically this means that I am able to utilize not only the password encryption scheme from Symfony2, but also to allow all users from the website it powers to immediately get access to their own XMPP accounts. The only downside is that I haven't found a way to link roosters, which means that the contact list in the chat client and on the website is not synchronized in any way. So users will have to maintain two lists of contacts.

All code is available on [GitHub](https://github.com/AmusableLemur/Destruktiv/blob/master/src/Destruktiv/UserBundle/Command/EjabberdCommand.php) as per usual. If you want to use this on your own project make sure that the ejabberd user has write access to `app/logs` and `app/cache`. If you just want an XMPP account you can create a user on [Destruktiv](http://destruktiv.se).
