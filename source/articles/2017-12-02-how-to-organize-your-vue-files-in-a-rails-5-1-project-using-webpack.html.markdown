---
title: How to organize your Vue files in a Rails 5.1 project using Webpack
date: 2017-12-02 17:47 UTC
layout: post
tags:
- vue
---

So, you're a Rails developer, and you started to play with Vue (maybe using the CDN / ES5 way?), everything looks so exciting, you're even thinking about using it in your next project. Great! And then problems start to pop up. How do I structure my files? How do I implement I18n? What about authentication? Pagination?... Surprisingly,
I did not found a lot of resources related to Vue+Webpack+Rails, so I thought it might be a good idea to share some of the solutions I came up with.   

**You'll find a demo app** repository [here](https://github.com/gbarillot/rails-vue-demo-app), so you could play with the code and test it out.

*Disclaimer*: I am not a "Javascript developer". I'm a Python -> PHP -> Ruby/Rails dev for 15 years, and this blog post is a highly opinionated way of solving common problems using a Rails 5.1+ back-end stack, primarily targeted for Back-end devs. who want to start building a SPA without being totally lost. If you see something atrocious in my code, feel free to shoot me an Email (or even better, ask for a PR on the demo repo). Thanks.

## 1. The specs

Let's start with what I really wanted for this demo project:

- Sprockets is not able to deal with ES6 code, nor .vue files, we'll have to use Webpack
- Pagination should work hand in hand with Kaminari
- Authentication, to access an Admin section
- Dynamic filters are mandatory in any Admin section, we should be able to use Ransack
- I18n is important, and it should be simple to use. Translations files are also rapidly growing up in a
real app, we should be able to handle this in a real world scenario
- ActionCable is great, we should also handle it
- A user should be able to reload any page at any time. Same for the back button that should just work.

## 2. Opinions and tools

- The directory tree of Javacript files should be scalable and easy to grasp. Maintainability above everything.
- Server side generated routes must match with the ones you'd get in regular Rails app, let's avoid headaches
- Avoid installing JS dependencies and plugins, as much as possible, except for what's officially supported/required by Vue
- Since most (actually: all) of the projects I work with are using Bootstrap, where it is required, let's use good ol' JQuery for AJAX requests
- CSS will be handled by the asset pipeline, "the classical way". Although you can add CSS inside of your .vue files, I can't find a single use case where it would be <strike>useful</strike> a good idea in the Web apps I build
- Vuex simplifies **a lot** of things, let's use it
- Components should not perform AJAX calls directly. Components should take care of "view layout + behavior", and nothing else
- Strictly speaking, server side generated JSON is an "API", but I won't build a pure RESTfull "API" here. I choose JSON builder for the demo, primarily because it is simple to actually see the JSON structure in the code, but feel free to use whatever tool is best for you. Anyway, I tend to think an "SPA back-end" != "public API", but that's another debate

## 3. How it works

Admitting you already initialized your Rails project with:

```
rails new myapp --webpack=vue
```

You should now have a "javascript" directory inside of "/app" and (awesome news!) you should get Webpack already setup with Vue.js and ready to roll. Let's now have a look at what we're going to put inside of this directory


#### 3.1 Base directory structure


```
/javacript
    /packs
        /components
            /home
                index.vue
        /filters
            string.js
        /vuex
            /stores
            index.js
        /application.js
        /routes.js
```

- components: will be structured quite close to what it would have been in the "view" rails dir, and will contains, well... components. Basically, your ".vue" files.

- filters: more or less like "helpers", in the Rails world. I use it to format strings, dates... more about filters [here](https://vuejs.org/v2/guide/filters.html).

- vuex: the "index.js" file is used to register stores and is mostly populated with "import" statements. On the other hand, the stores directory hosts all, namespaced, stores.

- applications.js: the main JS application boot loader, where you setup what you're going to use in the app (router, I18n...). This is where you setup I18n, and I also use this file to setup JQuery's AJAX calls

- routes.js: all of the routes for this app


#### 3.2 Loading the app

Let's load this app using [application.html.erb](https://github.com/gbarillot/rails-vue-demo-app/blob/master/app/views/application.html.erb), and since we're loading server side stuff, let's also load translations using a [small helper](https://github.com/gbarillot/rails-vue-demo-app/blob/master/app/helpers/application_helper.rb) that will translate the YAML file to JSON, so translations will be usable from Javascript. Right, doing it this way will imply a full page reload if the user changes its locale, but on the other hand you only load the current locale translations, and in the real world this is really important.

#### 3.3 Server side routing
At the very beginning of the project, routes are quite simple :

```
Rails.application.routes.draw do

  namespace :api do
    resources :dashboard, only: [:index]
  end

  root :to => "application#index"
  match "*path", to: "application#index", format: false, via: :get

end
```

What we're saying to rails here is that, except for what's related to the API, and for every URL we're requesting, always use the same controller and action. Why? Because we're going to use "real" URLs (why using #hashbangs when we have [HTML5 history!](https://caniuse.com/#feat=history)) so if the user reloads the page, we should always return the same file. What the user actually sees on the screen is now delegated to the Javascript app.

#### 3.4 Authentication

Simple: plain ol' Devise. Since this SPA is made to be loaded from a browser, there's no need to complicate things using JWT or OAuth for now. Authentication Data will be stored in a session cookie, which will be sent within AJAX requests.

#### 3.5 Adding a sub section (aka: and admin section)

In a traditional app, you would add and "admin" namespace in the controllers, and then an "admin" section in the views, right? That's exactly what we're going to do in the javascript dir:

```
/javacript
    /packs
        /admin
            /components
            /filters
            /vuex
            /application.js
            /routes.js        
        /components
        /filters
        /vuex
        /application.js
        /routes.js
```

Basically, what we're doing here is to create a totally separated "app", from a JS point of view. Doing it this way, you will load the Admin related stuff, and *only* the admin stuff. That means: routes, components, stores and while we're at it: translations. How do we load this JS app? Quite like we did for the front-end, but this time we'll use [admin.html.erb](https://github.com/gbarillot/rails-vue-demo-app/blob/master/app/views/admin.html.erb).

#### 3.6 File names conventions

Let's have a quick look at what's inside the demo's component directory:

```
/javacript
    /packs
        /admin
            /components
                /musicians
                    _form.vue
                    edit.vue
                    index.vue
                    new.vue
```

Feels familiar, isn't it? Classical names apply perfectly here, too. Files like "index.vue" or "edit.vue" are higher order components (aka: pages), where you import child components, underscore prefixed (aka: partials in the "old world").

#### 3.7 Vuex

If you don't know what Vuex is, I would highly recommend to watch those [2](https://youtu.be/dkFWOsKrPAI) [videos](https://youtu.be/kRI4YLMjgHQ). So, yes, let's use Vuex to handle all AJAX calls, as well as all state loads and modifications. If components may be seen like "views + behaviour", you can see a store quite like "controller + model". Controller because it handles the requests, and Model because it is manipulating the Data. Ok, ok, I know it's silly to try translating 1:1 Rails MVC to Vue, but if it may help you to understand how it globally works, let's see it this way to get started.

Ok, so, what's in a Store? Basically: [this](https://github.com/gbarillot/rails-vue-demo-app/blob/master/app/javascript/packs/vuex/stores/musician_store.js). Aside from the obvious actions + mutations, you will notice I added 2 extra mutations: progress and errors. This lead us directly to the next section:

#### 3.8 User interaction

One thing that is quite disturbing working with an SPA is that the browser is not helping us. There's no spinner at the top of the tab, and the page is not passing through the "click -> spinner is spinning -> refresh -> blank page -> repaint" cycle. Nonetheless, we have to take care of our user, and let him understand what's going on when submitting a form. That's why I created 2 extra mutations in stores that are using a form:

- progress: variable to track the current state of the request (start / loading / success / failed)
- errors: calls a [little helper](https://github.com/gbarillot/rails-vue-demo-app/blob/master/app/javascript/packs/admin/helpers/index.js) to show up form errors

A bit of CSS on top of that and now your users understand what's happening. You also avoid multiple form submissions, and this is not just a designer's whim.

#### 3.9 Kaminari

Pagination is made using a [component](https://github.com/gbarillot/rails-vue-demo-app/blob/master/app/javascript/packs/admin/components/shared/_pagination.vue), client side, as well as adding a short snippet in the server side generated [JSON](https://github.com/gbarillot/rails-vue-demo-app/blob/master/app/views/api/admin/musicians/index.json.jbuilder). Drop this component in a "/components/shared" directory, and now all you have to do is calling this in a parent component when you need it:

```
<pagination :pagination='pagination'></pagination>
```

(Hu hu, that's a lot of "pagination" for just one line, he? Don't worry, you'll found this pattern pretty common when passing data down to components).

#### 3.10 Ransack and dynamic filters

Quite like for pagination, the base idea is to sequentially:

- Update the query string using user parameters on form submission
- When a URL change is detected, call an action in the store using the Query string as an argument
- Request data from the server using this URL / Query string
- Finally, mutate the state with the data you just got back from server

What is a bit tricky here is that Vue sees query strings using arrays as JS Objects, so I had to tweak query string construction a little bit. In the end I got it working, now you just have to follow the steps to reuse [this component](https://github.com/gbarillot/rails-vue-demo-app/blob/master/app/javascript/packs/admin/components/musicians/_filters.vue) to fit your needs.

#### 3.11 ActionCable and Vue

You have to set things up exactly the same way you'd do in a classical app, the only thing we're going to add here is about informing Vue when new messages are coming. This is done using an Event Bus. With this Event Bus mounted, the [chat component](https://github.com/gbarillot/rails-vue-demo-app/blob/master/app/javascript/packs/admin/components/modals/chat.vue) will be notified each time there is a new event. On the other side, when you want to push new messages out, simply use the globally accessible "App" Object you created in the asset pipeline's powered [channel](https://github.com/gbarillot/rails-vue-demo-app/blob/master/app/assets/javascripts/channels/chat.js).

## 4. Packing it up

Wow, that's quite a lot of stuff for a blog post! I really encourage you to clone the demo [repo](https://github.com/gbarillot/rails-vue-demo-app/) and play with the code.

It's now time for to summarize some thoughts about building a SPA with Rails + Vue.js + Webpacker:

- **Rails is an awesome starting point for a SPA**: I read sooooo many tutorials and blog posts about configuring Webpack that I was terrified with this one question: "how and where do I actually start?". Now, with Webpacker and Yarn included right in the Framework, there's nothing to fear, everything works out of the box. Testing is also improved, since you can now test each.and.every.part of the backend, no need to spin up utter slow layers like Selenium to test views output, and testing JSON is trivial.   

- **Vue is a fabulous JS framework**: I feel like it has picked up the best ideas from React (Component based, Flux pattern) and the best ideas from Angular (templates with custom markup, eg: v-if, v-for...). Using Webpack to compile .vue files and Vuex, in the end, I managed to get something fully scalable as my code grows, and *really* maintainable with not that much of code, compared to a classical app.

- **A Single Page App is quite a weird beast**: The Web has not been built for SPA's, neither browsers were. Simple things in the "old world" may become quite tricky very fast (pagination+ransack, or even a simple form submission!), as in the same time complicated things now become easy as pie (updating the other side of the UI on the fly when a variable is updated in the store, for example). What I *really* appreciate is that the Javascript section is now under control. There's no longer JQuery soup boiling in the asset pipeline, with nasty and untestable bugs simmering in. If it was for one argument, it would be this one. Yes, it's worth writing a few more lines of code at the beginning. In the end, you'll win.
