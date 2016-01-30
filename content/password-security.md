---
date: "2016-01-20"
title: On password security
type: post
---

![LastPass](/media/lastpass.png)

Passwords are probably the biggest security risk that users face today. Most assume that a password that is *at least 8 characters long, contain upper case and lower case letters as well as at least one digit*. Problem is that this leads to passwords like *Password1*. But the *real* problem is that users believe that this password is so secure, since it technically follows the requirements for a "secure" password, that it can safely be used everywhere.

This is a huge security issue.

Surprisingly to some the use of a weak password is not the actual cause of distress, but rather that it's re-used everywhere. A stupid simple password like *Password1* might take five or ten attempts to guess, while a slightly more secure password might take hundreds or thousands of attempts.

But what about those super secure passwords that would take billions of years to find even with our most advanced computers today, passwords that look like "U0bVc@#VHFwvkJK&tY". Surely, those passwords would be safe to re-use?

The answer is actually no, absolutely not. It all comes down to website security. It doesn't matter if your password could guard Fort Knox if the website allows anyone to view and download your password.

And yes, this is actually more common than you think. Check out [*';--have i been pwned?*](https://haveibeenpwned.com/) for some famous security breaches. Even big players like Adobe, Forbes and Gawker have been vulnerable to attacks in the past. It doesn't even matter if the site encrypts your password or not, because you would have to trust every single site you use to use strong encryption.

This is why a weak password is not that big of a deal, to an extent. Even if the password might be guessed in a few hundred attempts it's not insane if it only grants access to one particular service and that service is not important to you. In other words, if you use a secure password for your banking and you use the same password for some online forum. Then if the forum gets hacked the hackers will automatically have the password to your bank as well. But if you use different passwords for every site they will only have access to the forum.

There are several ways to go about creating unique passwords for every site. One popular option is to use site-related passwords. If we continue from the previous example one such password might look like *Password1Facebook* for Facebook and *Password1Twitter* for Twitter and so on. While this would stop automated attempts it's still quite easy to guess what the password is for a different service.

Another option is a kind of compromise. You basically divide the websites and services you use into two or more security zones. In this case you have one password for each zone. The upside of this is that you only need to remember as many passwords as you have zones. If a password is compromised it only affects the other websites in the same zone. The downside is that multiple accounts can still be affected when only one is compromised.

The third option, and only if you want to feel completely secure, is to use a unique, strong password for each and every site or service. While this would prevent all attack vectors mentioned earlier it's a hassle to remember that many passwords which is the biggest downside of this approach.

Luckily this can be solved with a password manager. With a password manager you basically remember one ridiculously strong password to keep track of and safeguard all your other passwords. Most, if not all, password managers also have built-in functionality to generate secure passwords for you.

In selecting a password manager there are troves to select from. In my search I considered Keypass, Dashlane, Lastpass and 1Password (There are many more, but in my opinion these are your best choices). I passed on Dashlane and 1Password because they lacked Linux support which is a deal-breaker for me. Keypass is fantastic but doesn't integrate well with browsers and has no built-in synchronization between devices. Which is why I finally signed up for LastPass.

One of my favourite features is the *Security Challenge* it offers, where it makes sure that you aren't using duplicate, weak, or old passwords. It even scans known password leaks to give some warning if one of your accounts have been compromised. [*';--have i been pwned?*](https://haveibeenpwned.com/) mentioned above does this as well.

This brings us to the two final topics I wanted to discuss regarding password security. How to choose a strong password, and a brief explanation on what entropy is. They are tightly related and I'll begin with entropy.

Entropy is a measure of true (unpredictable) randomness. This is used in password security as a sort of score for how guessable your password is. The higher the score, the more random and unpredictable your password is and the more secure it is as a result.

Entropy is also the reason why you need so many weird letters in your password. If your password only uses lower case letters then that limits the number of possible combinations to `26^X` where `X` is the length of your password. Hence, a single character can only be one of the 26 letters, two characters can be combined `26 * 26 = 676` different ways, three characters `26^3 = 17,576` and so on.

If you add capital letters this is increased exponentially to `2,704` possible combinations for only two letters and `140,608` for three letters and so on. Adding numbers and special characters increases the possible combinations even further.

But this is not a measure of entropy. Entropy is randomness. If you choose an English word as your password you might have a password that is 10 or even 12 characters long. But in that case an attacker can just try every word in a dictionary to figure out your password.

This might not seem like a big deal, but when we have computers that can try a hundred billion possible password combinations *per second* it's not even a matter of microseconds. It's worth mentioning that these computers are not prohibitively expensive and most people with a gaming computer have this computation power already.

Explaining how entropy is calculated properly and what constitutes predictability would require its own article. I will just say this, anything you choose that helps you remember the password (dates, names, lucky numbers, etc.) reduces the security of your password.

This leads us to the final topic, how to choose a strong password. There are ways to choose passwords that are both secure, even by modern standards, and easy to remember. [Diceware](http://world.std.com/~reinhold/diceware.html) is my preferred option. You basically have a list of 7776 words which you use a die to select from (completely analog!). This gives you `60,466,176` possible combinations from only two words. `470,184,984,576` combinations from three words and so on. This would give som indication of how secure this is. And because of the way the brain works it's easier to remember words than letters, even when the words don't make any sense together.
