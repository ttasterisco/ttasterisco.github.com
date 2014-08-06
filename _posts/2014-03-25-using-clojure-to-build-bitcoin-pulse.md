---
layout: post
title: Using Clojure to Build Bitcoin Pulse
summary: The architecture of bitcoinpulse.com
---

[Bitcoin Pulse](http://www.bitcoinpulse.com) is a website that lists a varied number of metrics related to the Bitcoin ecossystem.
It tracks the price, number of wallets in the most popular services, number of tweets, number of wikipedia pageviews, etc etc.
The first alpha version was essentialy built in about 10 days and presented by myself at [San Francisco's Bitcoin Meetup](http://www.meetup.com/...) group in November xx.
The website was [publicly announced](http://news.ycombinator.com/thread?id=) in December xx. I have to say that most of the time was spent working on the frontend (and I can't say I'm proud of it).

The goal of this post.

### Clojure, Bitcoin Pulse and Me
The backend is entirely built in Clojure and this post serves to share how it works behind the scenes.
-describe previous clojure experience-

### Project Organization
I follow VERY loosely [Amit Rathore's Domain Driven Design](http://www.infoq.com/...)
It's great. It's the template I use for all my clojure projects.


### The Architecture
Bitcoin Pulse follows a bit the unix way. It is a number of semi-independent processes that are responsible for:
- collecting the data
- computing stats
- creating charts
- serving the data (the website)

#### Data Collection
The core of Bitcoin Pulse is the scraping and consumption of APIs from predefined data sources.
-img-
Scraping in clojure is pretty simple. Several tutorials explain how to use enlive to achieve this.
Consuming APIs is also rather trivial. httpkit is an excellent library for this...

Hitting the data sources happens one or multiple times at specific points of the day, depending on the data source.
Basically, tasks are scheduled using [chime](...).

The data model ...
korma

Thinking about the extensibility of the system, i.e. adding more data sources, I architectured the system to be ...
This way, adding a data source simply consists in the following steps:
- defining the model for this source
- writing the scraper/api consumer for the data source -example-
- adding this data source to the ... -example- I'm sure this could be simplified but I haven't spent much time thinking about it
- defining what should happen after the collection
- defining when the collection should occur

#### Computing Stats
...

#### Creating Charts
[incanter](...)

#### Serving the Data
ring app
clostache, ..., stencil
compojure
"load balancing"
nginx

#### Misc
bootstrapping data
logging [timbre](...)

### Deployment
...
git push

### Final Notes
Number of LOC
Possible Improvements

Suggestions?


Conception date: March 25th, 2014
