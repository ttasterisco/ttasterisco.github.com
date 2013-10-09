---
layout: post
title: How to deploy a Clojure/Compojure webapp in Heroku using lein ring
summary: Shameless SEO whoring.
---

And I'm guessing a great way to whore some search engine love.

## Sources/Useful Reads:
[http://stackoverflow.com/questions/17288537/heroku-deployment-error-w-compojure-could-not-locate-leiningen-core-classpath](http://stackoverflow.com/questions/17288537/heroku-deployment-error-w-compojure-could-not-locate-leiningen-core-classpath)

[https://devcenter.heroku.com/articles/clojure-web-application](https://devcenter.heroku.com/articles/clojure-web-application) ; they use a different model of deployment

[https://devcenter.heroku.com/articles/clojure](https://devcenter.heroku.com/articles/clojure)

## Target versions
For Clojure 1.5.1 and Compojure 1.1.5.

## project.clj
The `ring-servlet` dependency is required. You should also use lein2.

<pre>
<code class="clojure">
(defproject your-project "0.1.0-SNAPSHOT"
  :dependencies [
    [org.clojure/clojure "1.5.1"]
    [compojure "1.1.5"]
    (...)
    [ring/ring-servlet "1.2.0-RC1"]
  ]
  :plugins [[lein-ring "0.8.5"]]
  :ring {:handler your-handler}
  :profiles {
    :dev {:dependencies [[ring-mock "0.1.5"]]}
  }
  :min-lein-version "2.0.0"
)
</code>
</pre>

## Procfile
Create a [`Procfile`](https://devcenter.heroku.com/articles/procfile) for Heroku:

`web: lein ring server-headless $PORT`

## system.properties
Create a [`system.properties`](https://devcenter.heroku.com/articles/add-java-version-to-an-existing-maven-app) on the root of the project (same place as `project.clj` and `Procfile`) and add this into it:

`java.runtime.version=1.7`

## Deploying
In your shell, run the following commands

<pre>
<code>
  git init
  git add .
  git commit -m 'heroku deployment'

  ; assuming you have the Heroku toolbelt installed
  heroku login
  heroku apps:create

  git push heroku master

  heroku open
</code>
</pre>

And profit!

Conception date: August 15th, 2013
