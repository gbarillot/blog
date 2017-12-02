---
title: A better organisation for JS/Jquery code base using Rails and Coffeescript
date: 2014-08-15 08:59 UTC
layout: post
tags:
- ruby-on-rails
---

Once upon a time, there were two very, very distant planets... the first one was using brand new shiny full stack JS Frameworks, that handle rooting, templating, data binding. 
On this planet, apps were blazing fast, Javascript files were well organised and precisely structured
The second planet was generating plain HTML directly out of servers. Search engines were happily crawling tons of content, but there was no precise organisation for Javascript code. Ok, fine, but what about the real world,
 when you have to build bridges of features between the two planets? Well... deal with it.

In this post I'm going to explain how I ended up structuring my JS/Jquery based files in a regular Rails app. I'm not pretending that's THE way to go, it's just some simple tricks I use to keep things
 under control and manageable over time. I use Rails and its asset pipeline + coffeescript (and I love it!), but I guess it can be easily transposable to other stacks.

Ok, let's see some code!

#### 1. First try

*/app/views/tasks/index.html.haml*

*Note: as you may notice, I do not use the Rails remote: true method for forms. I'm just explaining my thoughts here, not trying to optimise, but you get the idea*

```haml
    = form_tag tasks_path, id: 'tasksForm' do
      = text_field_tag 'tasks[name]', '', id: 'newTask'
      = submit_tag 'Create'

    %ul#tasks
```

*/app/assets/javascripts/application.js.coffee*

```coffeescript
    $ ->
      #... Some code here....

      $('#tasksForm').submit -> (e)
        e.preventDefault()
        $.ajax
          url: $('#taskForm').attr('action')
          method: $('#taskForm').attr('method')
          data:
            task:
              name: $('#newTask').val()

          success: (data) ->
            $('#tasks').prepend("<li>"+data.task.name+"</li>")

      #... MORE code....

```

Ok, it works, but there are some problems with this code :

- CSS IDs are used as JQuery DOM identifiers
- Nothing is reusable, everything is enclosed inside the Ajax request
- Some HTML code is embedded inside Coffeescript
- At first sight, nothing tells me that the form will use AJAX
- As the app grows up the $(document).ready global listener will end up in a f*** huge, un-maintainable file

#### 2. Using data-attributes instead of IDs

This one is really important, by decoupling CSS presentation and JS behaviour. CSS ids and classes really shouldn't have nothing to do 
with JS. Let's start to clean things up:

*/app/views/tasks/index.html.haml*

```haml
    = form_tag tasks_path, data:{do: 'createTask'} do
      = text_field_tag 'tasks[name]', ''
      = submit_tag 'Create'

    %ul{data: {is: 'tasks'}}
```

*/app/assets/javascripts/main.coffee*

```coffeescript
    $ ->
      #... Some code here....

      $("[data-do='createTask']").submit -> (e)
        e.preventDefault()
        $.ajax
          url: $("[data-do='createTask']").attr('action')
          method: $("[data-do='createTask']").attr('method')
          data:
            task:
              name: $("[name='task[name]']").val()

          success: (data) ->
            $("[data-is='tasks']").prepend("<li>"+data.task.name+"</li>")

      #... MORE code....

```

Much better. Now I can see the form is using AJAX at first sight. Nonetheless, our "task" feature is still
mixed up inside the rest of the JS code. That's where Coffeescript and a few lines
of magic are going to help us.

#### 3. Splitting into components

*/app/views/tasks/index.html.haml*

```haml
    = form_tag tasks_path, data:{component: 'Task', do: 'create', on: 'submit'} do
      = text_field_tag 'tasks[name]', ''
      = submit_tag 'Create'

    %ul{data: {is: 'tasks'}}
```

*/app/assets/javascripts/main.coffee*

Here comes some secret sauce to bind Coffeescript classes, methods and events to our DOM

```coffeescript
$ ->
  # Listen to components' triggers
  $("[data-do]").each ->
    that = $(this)
    if typeof that.data 'on' != 'undefined'
      that.on(that.data('on'), (e) ->
        if typeof that.data 'component' != 'undefined'
          e.preventDefault()
          window[ that.data('component') ][ that.data('do') ]( this )
      )

```
What these lines are doing: each time there's a "data-do" attribute, bind the event listener described by the "data-on" 
so we can call the method name of the Coffeescript class described in "data-component".

*/app/assets/javascripts/components/tasks.coffee*

```coffeescript
    class @Task

      @create = (el) ->
        form = $(el)

        $.ajax
          url: form.attr('action')
          method: form.attr('method')
          data:
            task:
              name: form.find("[name='task[name]']").val()

          success: (data) ->
            $("[data-is='tasks']").prepend("<li>"+data.task.name+"</li>")

```

Bam! Now we have:

- A potential clear separation between our features, that we can place in distincts Coffeescript "components"
- A clean way to call and instantly identify how JS triggers are bind to there own event handler
- A better re-utilisability

#### 4. Decoupling request and presentation

We can now improve the rendering section, and decouple it from the request/response method: 

*/app/assets/javascripts/components/tasks.coffee*

```coffeescript
    class @Task

      @create = (el) ->
        form = $(el)

        $.ajax
          url: form.attr('action')
          method: form.attr('method')
          data:
            task:
              name: form.find("[name='task[name]']").val()

          success: (data) ->
            show(data)

    # Private
      show = (data) ->
        $("[data-is='tasks']").prepend("<li>"+data.task.name+"</li>")

```

#### 5. A little deeper?
<br />
##### HTML rendering
I didn't want to cover this aspect here, but you may have a look at [Transparency](https://github.com/leonidas/transparency), which allows you to build HTML
from templates within the existing DOM. Could be perfect for lists, for instance. Interesting and lightweight solution.

##### Turbo Links
I played a bit with this technique on a pet app using turbo links and it just worked perfectly. That may be an interesting and perfect fit to fill the gap
between the two planets (client side / server side).

#### Conclusion

While Angular, Ember and co. are all great solutions, they are *all-in-one*, by nature.
Now, if you just want server side generated content (one good reason for that could be SEO), and you only need to 
speed up some forms and add a bit of speed to your UI, you really have to take care of your JS code base before it explodes in an un-maintainable mess... 
from this perspective, I'm pretty happy with the organisation I explained here. Lightweight, maintainable, efficient. 


