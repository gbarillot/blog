---
title: 'Switch from Selenium+Firefox to Poltergeist+Phantomjs and speed up your test
  suite '
date: '2013-03-23'
layout: post
tags:
- la-technique
- ruby-on-rails
---

Selenium is a great tool for integration testing but it has two major drawbacks :*it relies on Firefox engine, so every time Firefox updates, you have to cross your finger and praise your test suite will still be usable


*it is f**** slow
Solve those 2 problems in just a few minutes, switch to phantomjs ! Phantomjs is a headless browser that uses a webkit engine, just grab the binary according to your plateform
[here](http://phantomjs.org/download.html). In my case (ubuntu 64 bits) , I installed it on my system this way :

$ tar jxvf  phantomjs-1.9.0-linux-x86_64.tar.bz2
$ sudo ln -s /home/guillaume/phantomjs-1.9.0-linux-x86_64/bin/phantomjs /usr/sbin/phantomjs
What just really matters here is that the binary should be accessible from your PATH.

Second step, for Rails users, install poltergeist to use phantomjs from your app :

# Gemfile
gem 'poltergeist'
...and then "bundle install".  You also have to change slightly your Rspec settings  :

# spec/spec_helper.rb
# Before :
require 'selenium-webdriver'
Capybara.default_driver = :selenium

# Change to :
require 'capybara/poltergeist'
Capybara.javascript_driver = :poltergeist
Ok, easy enough ? That'll all ! Enjoy your integration tests :

# Selenium
Finished in 35.52 seconds
14 examples, 0 failures

# Phantomjs
Finished in 18.47 seconds
14 examples, 0 failures
Yes, almost 2x faster :-)
