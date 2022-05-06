---
title: Rails 7 + Vite + Vue 3 + Pinia starter pack
date: 2022-05-05 14:36 UTC
layout: post
tags:
- vue
---

Let's face it, if you start a new Rails + Vue project you'll have to deal with an initial plumbing phase only to setup all the basic stuff. That's usually not the most fun part... but I have some good news: I did the boring work for you :-).

Having built and deployed two fairly large apps (>34K LOC) using the opinions and tools exposed in a [previous blog post](https://guillaume.barillot.me/2017/12/02/how-to-organize-your-vue-files-in-a-rails-5-1-project-using-webpack/), it was time to upgrade the whole stack up to 2022 standards and I wrote a new starter pack you can find here: [https://github.com/gbarillot/rails-vue-demo-app](https://github.com/gbarillot/rails-vue-demo-app).

## What you'll get in the demo app 
- Vite integration inside Rails through the Vite-Ruby gem
- Vue 3 + Pinia full setup and ready to roll
- Form animations, out of the box
- 404 and 500 error pages wrapped around the API and routers
- Server side + client side routers setup
- I18n setup
- Front / Admin namespaces
- Authentication using Devise
- Pagination and Ransack working hand in hand with Vue router 
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

## Why is the 2022 update better? 
- The Vue App setup is more consistent, easier to extend if you need it using "plugins" (examples included)
- Form animations are now 100% transparent, just use the "api" wrapper with the right HTML element
and everything will be handled automatically. 
- Thanks to Pinia, stores are now more compact and less verbose. They are also composable which could be usefull in some cases
- The "components" directory is now named "views". I noticed it in some Vue projects and that totally makes sense in order to bring Rails conventions into a SPA
- Although I didn't port big existing apps yet, I expect Vite to be way faster than Webpack. With a 
5K LOC Vue app the sluginess of Webpack started to be a problem in development
- Porting only the bootstrap grid (using native CSS Grid layout) lets you write custom CSS fast and efficiently without the whole Boostrap bloat. Anyway, feel free to use whatever CSS framework you prefer...
- No more JQuery for HTTP Requests, Axios does the job perfectly for a fraction of the load size

## How is it to work with a Rails + Vue stack since 2017?
Well... It works! We recently onboard a junior dev (first job, no previous experience with Rails nor Vue) and he's been really productive in just a few weeks. Even at > 34K LOC, we're still far from any "maintainability wall". Our UI is fast as hell, adding new features is still a pleasure and all of this is realiable and easily testable. 

Long story short: **a Single Page App doesn't have to be painful**.

Feel free to contribute, I'm open for questions or comments you may have! 
