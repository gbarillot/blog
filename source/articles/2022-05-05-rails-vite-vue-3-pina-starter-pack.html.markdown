---
title: Rails + Vite + Vue 3 + Pinia starter pack
date: 2022-05-05 14:36 UTC
layout: post
tags:
- vue
---

A blog post I published in 2017 about [how to organize your vue files in a Rails projet](https://guillaume.barillot.me/2017/12/02/how-to-organize-your-vue-files-in-a-rails-5-1-project-using-webpack/), ended with those words: "The Web has not been built for SPA's, neither browsers were. Simple things in the "old world" may become quite tricky very fast". Not only this remains true, but I should 
also add "Rails has not been built for SPA's neither". Let's face it, there is an initial plumbing 
phase were you have to setup all the basics if you want to use Rails + Vue & friends.

Having built and deploy two fairly large apps (>34K LOC) using the opinions and tools exposed in the [previous blog post](https://guillaume.barillot.me/2017/12/02/how-to-organize-your-vue-files-in-a-rails-5-1-project-using-webpack/), I wanted to upgrade the whole stack up to 2022 standards and wrote a new starter pack you can find here: [https://github.com/gbarillot/rails-vue-demo-app](https://github.com/gbarillot/rails-vue-demo-app).

## What you'll get in the demo app 
- Vite integration inside Rails through the Vite-Ruby gem
- Vue 3 + Pinia + Vue router + Vue I18n full setup and ready to roll
- Form animations, out of the box
- 404 and 500 errors pages and handlers working with the API and routers
- Server side + client side routers setup
- I18n setup
- Front / Admin namespaces
- Authentication (using Devise)
- Websockets bindings with ActionCable
- One basic CRUD example 
- A Bootstrap like grid using native CSS Grid

## What changed since 2017
- Rails 7 no longer uses Webpack
- Vite is now the prefered compiler for Vue projects
- Pinia replaces Vuex
- Boostrap has gone (even more) bloated
- CSS Grid layout browers support is now mainstream
- Axios is largely used in SPA based projects

## Why is the update better? 
- The Vue App setup is more consistent, easier to extend if you need it
- Form animations are now 100% transparent, just use the "api" wrapper with the right HTML element
and everything will be handled automatically. 
- Thanks to Pinia, stores are now more compact and less verbose
- The "components" directory is now named "views". I noticed it in a few Vue projects and that totally makes sense in order to bring Rails conventions to a SPA
- Although I didn't port big existing apps yet, I expect Vite to be way faster than Webpack. With a 
5K LOC Vue app the sluginess of Webpack started to be a problem in development
- Porting only the bootstrap grid (using native CSS Grid layout) lets you write custom CSS fast and efficiently without the whole Boostrap bloat. Anyway, feel free to use whatever CSS framework you prefer...
- No more JQuery for HTTP Requests, Axios does the job perfectly for a fraction of the load size


Feel free to contribute, I'll listen to any question or comment you may have! 
