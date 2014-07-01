---
layout: post
title: My Experience Building a Frontend Web Application with Om and core.async
summary: In which I analyze the journey of creating a clojurescript/om/core.async app.
---

In which I analyze the journey of creating a not-so-simple but
also not-that-complex web application in Clojurescript using Om
(Clojurescript's port of React.js), core.async and other tools.

## Backtracking

The goal of this project was to showcase a few of my Ring libraries. Having an
example that bundles everything is always very useful, not only for those
looking for something with a potential "production" feel, but also for me - the
creator - in understanding new perspectives and trying out alternative things.

While building the backend was a rather quick process, building the frontend
was an open problem. Which was a good thing, as it allowed me to explore
something new. Thus Clojurescript and Om.


The world-changing artifact that was built was a note taking application.
[Check the demo.](https://clj-notes.herokuapp.com)

Looks simple, right? It's basically your typical CRUD program. But the devil
has always been in the details, not in the 10000 foot view.

It is a Single Page Application, meaning that all communication with the server
(after the initial load) is done asynchronously.

It allows for user sign-in/up, creating notes with a private or public
visibility, changing the visibility, deleting notes, retrieving a single note,
retrieving all of the user's notes and retrieving all of the public notes.

So you can deduce that authentication and authorization are bolted in (try
viewing a private note in an incognito window), but also client side routing
(the pervasive hash when navigating between different "pages"). And if you
navigate around the app, you'll notice the "Loading" placeholder while the app
waits for the content to arrive.

But these are only the superficial details. Now let us dive into the
technicalities.

## [Clojurescript](https://github.com/clojure/clojurescript)

- The experience of working with Clojurescript ; TODO
ah, namespaces... such niceness

- Clojurescript if you know Clojure vs Clojurescript if you don't know Clojure ; TODO

- What Clojurescript fixes (vs Javascript) ; TODO

- What Clojurescript doesn't fix ; TODO

### A detour into writing Javascript in Clojurescript
; TODO
- that was my first approach
- manually manipulating the DOM
- using jquery equivalent code
- callbacks everywhere
- pros: very fast to build (experience in javascript)
- cons: things are very tightly coupled (and why that is bad)

Now back to Om...

## Om and core.async

- What is Om ; TODO
[Om](https://github.com/swannodette/om): ClojureScript interface to Facebook's
React
- How React/Om works: components, components, components ; TODO

- What is core.async ; TODO
[core.async](https://github.com/clojure/core.async): Facilities for async
programming and communication in Clojure(Script)

- What Om isn't ; TODO
Note that React.js is not a full blown javascript framework.
Om, in the current state, cannot be considered as a cljs framework either.
Unfortunately, as we'll see, there's going to be the tendency to use it as such
(pet peeve: perhaps it should be a good idea to rename app-state to view-state).

- Why Om? ; TODO
But React/Om have many other advantages - the main one is the virtual DOM that
frees developers of having to manually update the UI when changes occur and has
a very good performance when rendering in the browser.


### How do Om and core.async play together? And why do it?

- Separation of concerns: having components talk indirectly
(maintainability, reusability, future changes) ; TODO

- TODO: explain how does Om and core.async glue to each other



### Critique: When OO meets FP

React.js makes full use of javascript's "OO". React components are simply
javascript objects with a strictly defined lifecycle.

Since Om is based on React.js, it feels very impure. Mapping the component
lifecycle model to Clojurescript is trying to fit OO into FP.
It simply doesn't feel clean. (TODO: example of how it doesn't feel clean)

The best examples of this impureness are that Om brings the direct state
manipulation through `transact!` for application level state and `set-state!` for
component level state. Or `get-state` to access component state or even *gasp*
`get-shared` to access data that is shared accross all components of a tree.

It just goes strongly against FP's ethos where we expect the data to be
passed to us as arguments and passed back to the world as return values
and not have side effects.
It would be "ok" if we did not have to make use of these functions, but
unfortunately there is no escape - transact! and set-state! are the de-facto
way of doing things in Om.

TODO: explain how the philosophy is to contain global state change
that's why we have cursors passing the correct data into components


### Critique: Channels

Channels are a nice way to have parent<->child or sibling component
communication in Om at a small scale.

; TODO
-Why parent-child and siblings and not between non-directly related components?
Due to the tree structure of React components, passing the channel of a parent
component to some other component requires passing the state through the
component build process. Or using application or shared state.

Also due to the tree structure, the channel creation process is not really
clean - if the child ever wants to communicate with the parent component, this
must be known by the parent, so it can pass a chan in :init-state (either that,
or the child component has to keep checking if a channel was handed to it).
Ugh! Can you imagine the nightmares of "component reusability" that React/Om are
touting? (TODO: example code) Just because some 3rd party component needs a
channel to communicate something not-really-important-for-my-use-case,
I, in my parent component, must setup everything for this communication to
happen. In a nicer world, things would be returned by (build ...) and the
parent component would do as it pleased.

; TODO
-Why small scale only? By small scale, I mean that any given component should
only be communicating to one other component unless you want to deal with
taking care of things for multiple channels or demultiplexing the communication (TODO: correct term?)

Example: component has two buttons, each does something over the wire, so a
response from the network is expected (the network or whatever it is you're
using to abstract it). When the response comes, you'll want to do something to
the UI - Om suggests doing it in IWillMount. This is the code you'll have to
write:

(TODO: the code of channel creation/retrieval, communication handling, etc)

Can you imagine this for 5 channels? Or talking with 5 components (which will
have to be in a unidirectional way lest you want to further complexify your
communication processing logic).


; TODO: this isn't really the case - see latest code where channels are created
; in place and thus not immediately allocated but only when an event happens
Another point of contention for me is that using channels in UI programming
doesn't feel very resource efficient (no matter how lightweight channels are, (TODO: link to David Nolen's 10000 updates etc post)
and I know they are). Example: if a child component is handling some event
that will require the parent component to update things, you'll have to either
use a callback or channels. Now imagine 100 child components - do we really
want to establish communication between parent-child so many times? Even if
this event will be rarely triggered? Concrete example: a delete tweet button on
a tweet item that belongs to a timeline that consists of a very large number of
tweets. This feature will hopefully be rarely used, as such there's no need for
a checkbox in each tweet so the user could do mass-operations. But it might
still happen a few times so it's nice to have the button there in the item.

That's how bad it feels.

; TODO
Yet, I might have preferred channels as a way of transmiting changes to the
application and component state instead of set-state/transact! just to maintain
some level of pureness.

### Critique: Dear Om
It would have probably been more interesting to have Om do everything through
channels instead of using the state manipulation functions.

In the end, the question should be: is it possible to run away from the callback
model? Not with the current set of tools. Callbacks are native to the way
browsers work (event handlers)





## Architecturing Om apps

TODO: there's no defined way yet of laying out the parts of an Om app
TODO: Omchaya

### It all starts in the Beginning

; TODO: main.cljs and `teh-app` component
; what is done at the wiring
; how teh-app works (render-state)


### Frontend Routing

TODO: multiple event sources (a href, user changes location, internal app state change)
TODO: how Secretary is used


### Server Communication
One immediate question when developing the frontend of a web app is: where am I
going to put the code that interacts with my remote server?

Om doesn't really have an answer for this. React suggests putting the code in
IWillMount with the functions being added to the component itself. Apart from
the bold ...? TODO: ?
But because Om maps React's components into protocols, React's suggestions was
lost in translation (TODO: was it??)

TODO: explain this better
Om added a feature called tx-listen that allows for the observation of
app-state changes (transation!).
David Nolen's om-sync makes use of this (TODO: does it? I think it does) by
tagging transaction!s that need to be synced to a server with a
:create/:delete/:update.

Unfortunately this use case is very limited - in real applications you'll want
more control over what operations you'll make with the server (TODO: examples?)

; TODO:
- my solution: control.cljs (this file really needs to be renamed)
- encapsulate all server communication
- using cljs-http instead of cljs-ajax (core.async vs callbacks)
- shared sidestream channel between components
- the need to create a communication "protocol"
- giant switch-`case` for dealing with communication
- count how many endpoints I hit
- speculate if this could be simplified with cljx?



### "Page" Components and "View" Components
; TODO: rename the files
- explain what I mean by page components
- explain what I mean by view components
- explain the existing page components
- explain the existing view components
- note-view: an example of a page component that reuses a view component
- handling DOM events
- communicating with "teh-app" and the server module

### The Development/Release Workflow
; TODO:
- explain the cljsbuild in project.clj
- integrating with external javascript (externs)
- things I don't like: SPAs vs MPAs vs Isomorphic (link to DomKm's blog post)
- cons of SPAs: preamble vs reusing assets (e.g. react.min.js)


## Finale
; TODO:
- I think Clojurescript is great. Since I'm not annoyed by superficial things like parenthesis
(I was already sold on Clojure), the benefits that Clojurescript brings are enormous
- Om/React's benefits are tremendous (virtual dom, instant render) despite all the shortcomings
- Using channels to communicate between components is a very good thing when building not-so-simple
applications


