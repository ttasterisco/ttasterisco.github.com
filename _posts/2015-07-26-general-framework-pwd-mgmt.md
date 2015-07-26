---
layout: post
title: A General Framework for (Strong) Pass Management
summary: My pass is stronger than yours. For non-technical people.
---

Well, I had this in my mind for months but about a month ago someone [kinda beat me to it](https://news.ycombinator.com/item?id=9744058).
And in less words too. That's what you get for being lazy. \*sigh\*<br/>

Anyway...


(I hope) This is an informative post for non-technical people.<br/>
Thought I should write this down since it's a pretty useful thing and not widely spread.<br/>
Do note that I am not a security expert. My name doesn't start with a R, S or A.<br/>
Please discuss in the comments section how bad my advice is.<br/>
kthxbye.



## Pick a Pass(word)

The web is full of articles teaching you how to pick a strong pass. And that's fine for a single website.
But what they don't teach you is how to pick a strong pass for the 10+ websites you visit frequently (and infrequently).

While there are solutions to this, e.g. using a pass management software (I like [LastPass](https://lastpass.com/)), for some reason the solutions might not be applicable to you.

So here's a general framework for picking strong passes and being able to remember them all (or almost!).



## Passes

Let's start with the *obligatory xkcd*:

[![Obligatory](http://imgs.xkcd.com/comics/password_strength.png)](http://xkcd.com/936/)

First of all, don't use pass**words**, use pass**phrases**. Or at least try to, since some websites are still stuck in the '90s.


### A. Generating a pass

This general framework lays on three things to generate your pass: a **phrase**, a **contextual keyword** and a **scheme**.

The scheme and the phrase are elements that you'll reuse whenever you're generating a pass.<br/>
The contextual keyword will be your variable element.

The end result is a unique pass for each site that should be fairly easy to remember.

#### 1. Long passes
The general consensus is that the best passes are long. The longer the better (heh). That's why passphrases have been gaining popularity.
But there's a catch: the words in your passphrase should be random or more correctly, with a low probability of them appearing next to each other. [^1]

[^1]: Kinda! There are ways to jump through this using a good scheme.

Another but! Some websites have a ridiculous low length limit for passes. They suck and you should think about not using them (yes [Skype, I'm looking at you and your 20 chars limit](http://community.skype.com/t5/Security-Privacy-Trust-and/What-does-the-skype-password-want/td-p/48790)) or [telling them how dumb they are](http://community.skype.com/t5/Security-Privacy-Trust-and/Remove-password-length-limit/td-p/1323100).

So, I'll (kinda) go against what the pros are saying and actually recommend you to pick a (long) phrase that you will be able to remember.
You should try and find something as unrelated to you as possible to avoid targeted attacks.
An example of a phrase would be "`you say goodbye and i say`" and you not being a Beatles fan.

#### 2. Pick a contextual keyword
I define a *contextual keyword* as **a word that you can derive from the website where you intend to use the pass**.

It can be something easy but you should pick the contextual keyword in a fairly consistent way (i.e. in a similar way in all the websites) so that if you have to sign in to some website you haven't visited in a long time, you can still guess what's the contextual keyword. It could be the first two words you see on the title, the name of the website, etc.

#### 3. Pick a scheme, i.e. a transformation method
So here's where the magic happens. I define a *scheme* as a **transformation that you apply to your `phrase + contextual keyword`**.

The scheme can be something like adding an alphanumeric character (e.g. `+`, `-`, `*`) or numbers between all the letters or words of your pass and have the 1st and last characters capitalized.

This adds a lot of complexity when trying to crack your pass, because it isn't sufficient for the attackers to use a dictionary to generate a phrase.
They'll also have to find out the scheme you used. So the more randomness your scheme creates, the better.

#### 4. Generating the final pass
So finally, this is how you'll generate your pass:

```
pass = scheme(phrase + the contextual keyword)
```

Example:

*initial phrase*: `yousaygoodbyeandisay`<br/>
*contextual keyword*: `islandofatlas`<br/>
*scheme*: `capitalize the first character and add a + as a suffix`<br/>

*resulting pass*: `Yousaygoodbyeandisayislandofatlas+`

But what about those websites with stupid length limits?<br/>
Huh... well, you can always shorten your phrase.<br/>
Sorry, that's the best I have. They suck!


### B. Changing the pass

There will always be situations where you will want to change your pass. Either because they got hacked or somehow you got hacked. What to do in those situations?

#### Changing everywhere
You can either change your scheme or perhaps pick a new phrase.

#### Just one Place
You can pick a new contextual keyword.



## Nothing is Safe

#### So, is this going to be a perfect way to never get hacked?
Unfortunately, no! There are several different vectors from which an attacker can get to you. But this should protect you fairly well.

#### And will you never ever forget a password again?
Unfortunately, no! You'll eventually forget a contextual keyword, but that's ok, that's why the "recover password" exists :)

#### Weaknesses

As gvb says in the HN post,

> *[T]hey likely won't see your pattern.* is the weakness in this system. There are bad web sites that still do not encrypt your password, in which case a hacker will see your pattern. There are many web sites that use poor encryption practices in which case a hacker can brute force decrypt your password and see the pattern.
>
> Once an attacker guesses your pattern, it is game over.

truedat. There is no good solution to this except generating good random passes that are very distinct for each service you use. Or avoiding crappy services.


#### More

Here's another guide to strong passphrases from which you can derive some utility [https://firstlook.org/theintercept/2015/03/26/passphrases-can-memorize-attackers-cant-guess/](https://firstlook.org/theintercept/2015/03/26/passphrases-can-memorize-attackers-cant-guess/).


At the end of the day, it's all about trade-offs. If you can't use a pass management software and you have to be the one generating and storing them, then I think this is probably your best solution.



Conception date: January 7th, 2015
