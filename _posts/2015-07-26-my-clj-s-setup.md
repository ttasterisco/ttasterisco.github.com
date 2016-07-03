---
layout: post
title: _My_ Clojure/Script Workflow
summary: Mine. Mine. Mine. Mine. Mine.
---

Yes, I was inspired by [this post](https://howistart.org/posts/clojure/1).
So read on to learn about an unpopular (why yes, I think so) way to do things.


## The Setup

These are the tools I use

* Linux ([Ubuntu GNOME](https://ubuntugnome.org/) at the moment)
* Sublime Text with [Enhanced Clojure](https://packagecontrol.io/packages/Enhanced%20Clojure) and [lispindent](https://packagecontrol.io/packages/lispindent) packages
* [Terminator](http://gnometerminator.blogspot.com/p/introduction.html) for my terminal needs (heh)
* [Nemo File Manager](https://github.com/linuxmint/nemo)

So there's the crux - I **don't** use Emacs. *\*ducks for cover\** There, I said it. *uff*. Ironically, I was an Emacs user for a few years, before I started with Clojure. But then I found Sublime Text and have been happy ever since (which doesn't mean I'll be faithful, heh).

I'm not listing [leiningen](http://leiningen.org/) since that's pretty much the default, but I am curious about [boot](https://github.com/boot-clj/boot).


## The Process

It's a simple one:

* I open up Nemo and enter my work directory
* I right click on a blank space and select `Open in Terminal`, which will bring up a Terminator window at the current dir
* `subl .` (so that Sublime opens up under the current path) or just regular launch Sublime if I was here before (it reopens with all the tabs from the previous session)

Off we go!


## But Now What?

Well, now it depends on the project I'm working on! I might split my Terminator into 2 or 3 terminals, maybe `ctrl + shift + t` to open one in a new tab, `lein repl` in one of them, launch whatever I need in the others: `lein ring server-headless`, `lein cljsbuild auto`, maybe `docker-compose up` something.

See, it's very dependent on the needs of what I'm doing.

In Sublime, I prefer the Single layout for maximum focus, but sometimes I'll `ctrl+shift+2` to get a 2 column layout and place a file I need to read in the 2nd column.

And Nemo supports multiple tabs too! So one tab for the root of the project, another tab for a subfolder in `src`, another tab for another subfolder in `src`, etc!

Need to open some file in Sublime that's in some obscure subfolder of the current path but you don't want to browse around Nemo? `ctrl+p filename` should do the trick.

That's it. Now just code away.


## Why?

So why this workflow instead of the traditional Emacs with Cider or something else? Well, because it works for me. It's the workflow that I've ended up with, not just for Clojure, but for other stuff too (like writing this post).

### Where Emacs+CIDER > My Setup

To be honest, I haven't tried the latest incantions of Emacs, so I really can't make a fair comparison (yes... shame on me, I know, I know) [^1].

[^1]: I mean, I've seen others using Emacs with CIDER, but have never actually gone through the experience. Back in the days when I started, there was no CIDER and CounterClockwise was actually my favorite editor (unfortunately Eclipse's "heaviness" drove me away).

There are definitely some nice things with CIDER that my setup doesn't provide: being able to cursor freely around the REPL is so cool, the auto-complete totally wins, and of course, the fact that you can hack Emacs in a easier way than Sublime.

But that's all ok. I'm past the phase of typing fast and less. Now, I'm just worried about what to type.

### Where My Setup Rocks

What I particularly enjoy about my setup is that it's pretty good for multiple monitors. Sublime on my main screen, Terminator on another. And maybe the browser on a 3rd screen.

And you can use the mouse (*can*, not *must*).

Also, it's a fairly lightweight setup too (well, I didn't audit it, but it sure *feels* lightweight).



### Boom!

So, if you want an alternative setup for using Clojure/Script, here is one.
It should be pretty easy to customize it, given that I use very specific tools for each job.

The end!


Conception date: April 5th, 2015
