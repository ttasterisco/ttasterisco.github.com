---
layout: post
title: Clojure Tips
summary: Stuff that I'm learning.
---

;;; change the configuration of your project by applying various profiles
https://github.com/technomancy/leiningen/blob/master/doc/PROFILES.md

;;; static code analyzer for Clojure which uses core.logic to search for patterns of code for which there might exist a more idiomatic function or macro
https://github.com/jonase/kibit

;;; Leiningen plugin designed to tell you your code is bad, and that you should feel bad
https://github.com/dakrone/lein-bikeshed

;;; Eastwood is a clojure lint tool which uses the analyze library to inspect namespaces and report possible problems
https://github.com/jonase/eastwood

;;; Leiningen plugin to run cloverage test coverage
https://github.com/lshift/cloverage/tree/master/lein-cloverage

;;; Clojure library for driving a web browser using Selenium-WebDriver as the backend
https://github.com/semperos/clj-webdriver

;;; destructuring http://blog.jayfields.com/2010/07/clojure-destructuring.html
(defn destruct-args [{a :a b :b c :c}]
  (println a)
  (println b)
  (if c
    (println c))
  )

;;; for with while break
(defn for-condition [x break-when]
  (not (= x break-when)))

(defn test-for-while [break-when]
  (for [x (range 100) :while (for-condition x break-when)]
    (println x)))

(test-for-while 10)

;;;





















