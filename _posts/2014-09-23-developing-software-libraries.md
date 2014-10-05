---
layout: post
title: Developing Open Source Software Libraries
summary: AKA User Experience for Software Libraries.
---

As I started reinventing the wheel in Clojure (writing a few libraries for backend web development), I actively became aware that I should think about the philosophy <i>behind</i> the libraries.
By that, I mean the general direction and goals of the development process, something that should guide and be the goal of all kinds of software libraries [^1].

[^1]: While I was unconsciously aware of the requirements and goals, this passive kind of thinking is fuzzy and can get dilluted along the way.

I don't think enough is written about the subject of creating software libraries, even though it might be the most popular artifact on github.
It is simply expected that the thoughts are present when the code is written and that the result follows.

So here am I, trying to change that [^2].

[^2]: Even though there are way more qualified people to do that.

## The Characteristics of a Good Software Library

A software library is a reusable piece of software that someone is going to import into a software project.
We use libraries because it saves us the trouble of writing code that can be abstracted by a third party and, thus, be reused.

I will be describing sets of characteristics that libraries should have to be considered "good" [^3].

[^3]: This doesn't mean that libraries that fail to satisfy these characteristics are not useful.

### _User Developers_ and _Programming Developers_

I begin by making a distinction between the two extremes of developers. It is by these points of view that we shall focus.

* _User Developers_ are programmers who are simply incorporating the library into a project, with little to no interest in the internals.
They probably make up the largest slice of the userbase;

* _Programming Developers_ are programmers who are interested in knowing how things were made.
This can be, among other reasons, due to simple curiosity but also idea gathering/refinement or interest in contributing back.

_Programming Developers_ should be viewed as (mainly) a superset of _User Developers_.

### From a _User Developer's_ POV
When searching for a library, users will be interested in the one that solves the problem and delivers the most _bang for the buck_.
Remember that the goal is to have the user not write the code for the functionality that the library is supposed to provide.

As such, the four characteristics that I deem as the most meaningful are:

* **_It solves the problem_**. This might be too obvious, but it is to serve as a reminder that the core problem you're trying to solve is the most important thing.
But it is also a reminder for not trying to do too much. While doing too much _might_ in a library be more about style than substance, so far the UNIX way has prevailed [^4].

[^4]: I am actually curious and interested in seeing at cases that are opposite of the UNIX way.

* **_It is efficient_**, whatever that means in the context of the problem. Again, this is obvious and it is expected by the users.
It also follows from the previous point that we might hit a crossroad when building a library, where we have a chance to go deep or go wide.
At a certain level, going deep starts getting harder and harder (micro-optimizations).
Going too wide though, might become a maintenance hell and lead to complete refactorings or starting from scratch.

* **_It is not hard to use_**. How hard is it to use your library? Does it provide a consistent interface and no unexpected gotchas?
How many functions or classes must the user be aware of? Sure, documentation helps a lot, but it would be great if most things could be avoided altogether (YMMV).<br/>

* **_It is not hard to reason about_**. How hard is it to understand what your library is doing? Is it clear what problems you're targeting?
Are you leaking implementation details to the user? How many new concepts do you introduce to a first time user?
This happens mostly with libraries that abstract some underlying technology, e.g., a library for AWS or for a database.
Try simplifying what's under you but also the interface that you provide to the user.

Remember, most people using your library will fall into this category. Attack these points and you'll make a lot of people happy.

### From a _Programming Developer's_ POV
A programming developer will always dive into the code. They are interested in knowing how things work.
So how can we help them with a smooth dive?

In practice, it's all about following good programming practices. A software library is just like any other medium/large software artifact.
One should aim for a codebase that is **_easy to read and understand_** and **_easy to change_**.
Apply modularity, low coupling, high cohesion, comment your code, write documentation - the whole shebang.

While commenting your code helps, when trying to understand a new codebase, it helps a lot to have architecture documentation, i.e., something explaining how the pieces are tied together.
This is something most open source software projects fail at, perhaps understandably, due to the boring nature of writing documentation.

So the best way to help programming developers is to write good code and documentation. Worried? Don't be.

## Nature vs Nurture
I don't think that it should be expected for a software library to be "good" at v0.1 or &lt; ~100 commits [^5].
A software library might not be born good, but it can surely grow into a good library.
And that's what we should strive for.

[^5]: Why 100? Sounds like a reasonable number. YMMV.

Conception date: June 1st, 2014
