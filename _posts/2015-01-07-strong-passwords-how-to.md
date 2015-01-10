---
layout: post
title: A General Framework for (Strong) Password Management
summary: My password is stronger than yours. For non-technical people.
---

DISCLAIMER
This is more of an informative post for non-technical people instead of the general theme of this blog.
Thought I should write this down since it's a pretty useful thing and not widely spread.
Do note that I am not a security expert. My names do not start with a R, S or A.
Please discuss in the comments section how bad my advice is. kthxbye.

The web is full of articles teaching you how to pick a strong password. And that's fine for a single website.
But what they don't teach you is how to pick a strong password for the 10+ websites you visit frequently (and infrequently).

While there are solutions to this - e.g. saving the password in the browser, using a password management software - for some reason those solutions might not be appliable to you.
So here's a general framework for picking strong passwords and being able to remember them all (or almost).


So let's start:

[http://imgs.xkcd.com/comics/password_strength.png](http://xkcd.com/936/)

A. Generating a pass

This general framework lays on three things to generate your final pass: a phrase, a contextual keyword and a scheme.

The scheme and the phrase are the elements that you'll reuse in the process. The contextual keyword will be your variable element.
The end result is a unique password for each site that should be fairly easy to remember.

1. Long passwords
The general consensus is that the best passes are long. The longer the better. That's why passphrases have been gaining popularity.
But there's a catch: the words in your passphrase should be random or more correctly, with a low probability of them appearing next to each other.
Kinda! There are ways to jump through this using a good scheme.

Another but! Some websites have a ridiculous low length limit for passwords.
They suck and you should think about not using them (yes Skype, I'm looking at you and your 20 chars limit).

So, I'll go against what the pros are saying and actually recommend you to pick a phrase that you remember.
You should try and find something as unrelated to you as possible to avoid targeted attacks.
An example of a phrase would be "you say goodbye and i say".

2. Pick a contextual keyword
I define a contextual keyword as a word that you can derive from the website where you intend to use the pass.

It can be something easy but you should pick the contextual keyword in a fairly consistent way (i.e. in a similar way in all the websites) so that if you have to login to some website you haven't visited in N months, you can still guess what's the contextual keyword. It could be the name of the website, the first two words you see on the title, etc.

3. Pick a scheme, i.e. a transformation method
So here's where the magic happens. I define a scheme as a transformation that you apply to your pass+contextual keyword.
The scheme can be something like adding an alphanumeric character (e.g. "+", "-", "*") or numbers between all the letters or words of your pass and have the 1st and last characters capitalized.

This adds a lot of complexity when trying to crack your password, because it isn't sufficient for the attackers to use a dictionary to generate a phrase.
They'll also have to find out the scheme you used. So the more randomness your scheme creates, the better.

4. Generating the final pass
So finally, this is how you'll generate your pass:
pass = scheme(the phrase + the contextual keyword)

So, to recap

initial phrase: yousaygoodbyeandisay
contextual keyword: facebook, google, youtube
scheme: capitalize the first character and use a +

pass: Yousaygoodbyeandisayfacebook+, Yousaygoodbyeandisaygoogle+, Yousaygoodbyeandisayyoutube+




B. changing the pass

<why>

1. everywhere
you can change: the scheme, the phrase

2. just one place
change the contextual keyword






is it going to be a perfect way to never get hacked?
unfortunately no! there are several different vectors from which an attacker can get in
but this will protect you fairly well. a long pass will make sure it's tough to crack

will you never ever forget a password agian?
no! you'll eventually forget a contextual keyword, but that's ok, that's what the "recover password" page is for

