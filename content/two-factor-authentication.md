---
date: "2014-02-07"
title: On two factor authentication
type: post
---
I'm studying computer security this term and it has a way of making you very paranoid about security matters, and recent articles like [this](https://medium.com/p/24eb09e026dd) and [this](http://arstechnica.com/security/2014/01/how-i-almost-lost-my-500000-twitter-username-jb-and-my-startup/) really doesn't help either. Therefore I've decided to set up two-factor authentication everywhere possible to help protect myself to some degree for the uselessness of passwords.

Two-factor authentication essentially means that you use two authentication factors to log in instead of only one. An authentication factor is one of three things, something you *know*, something you *have* or something you *are*. A password is a good example of the first, while a card or cell phone is in the second category.

What this means is that for someone to hijack one of my accounts they will not only need to know my password but they also need my cell phone to generate a temporary one-time key to log in. While my phone can also be remotely tracked and locked down in case it's stolen, and through backed up recovery keys I will still be able to access my accounts.

It might sound complex and difficult but it really isn't, and the major security gain is a worthwhile trade off. To enable two-factor authentication you merely have to download an app (like [Google Authenticator](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=en) or [Authy](https://play.google.com/store/apps/details?id=com.authy.authy&hl=en)), use it to scan a QR code for the account you want secured and then you're done. The next time you log in on a new computer you open your app, get a key to type in and you're logged in as usual.

There's also fairly comprehensive list of [services which support two-factor auth](http://evanhahn.com/tape/two-factor-auth-list/).
