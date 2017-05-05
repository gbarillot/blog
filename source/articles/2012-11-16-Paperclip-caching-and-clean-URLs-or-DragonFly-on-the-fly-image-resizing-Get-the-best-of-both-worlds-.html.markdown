---
title: Paperclip caching and clean URLs or DragonFly on the fly image resizing ? Get
  the best of both worlds !
date: '2012-11-16'
layout: post
tags:
- ruby-on-rails
---

When it came across image manipulation using Rails, I had to make a choice : Paperclip to handle high traffic/popular websites, and DragonFly for privates, more confidential but also more evolutive applications.

Let's start with an example :# Paperclip typical image URL
/system/pictures/877/thumbnail/my_thumbnail_image_name.jpg?1352719049

# DragonFly image URL
/media/BAhbB1sHOgZmIjIyMDEyLzA5LzE0LzE3XzI0XzA0XzMyMl9BdXLDqWxpZV9DSEFVVkVBVS5KUEdbCDoGcDoKdGh1bWIiCjUweDUw
Paperclip resizes the image 
, then store the thumbnail on the file system, whereas DragonFly only upload the original image, as is, then resizes the image 
. Well... I don't like any of those two solutions.


**Paperclip drawback**
 : imagine you have a long time living and popular website, with thousands of cool members/users who have each uploaded their avatar. This avatar is stored in 3 sizes, say : original, 200x200 pixels and 50x50 pixels. Cool, and now what happens after 2/3 years of success, when the client redesign the whole website and the designer asks for avatars in 100x100 pixels ? Hu ?! You're good to dive into obscurs shell scripts using ImageMagick on the command line... Nightmare.


**DragonFly drawback**
 : each time you call an image, you call the DragonFly Gem. Ok, it has an internal caching system, but it _is_ slow. Plus you can forget Google Image indexation and search engine optimization with such an ugly URL (and good luck to convince your client it "doesn't matter"...)

I was stuck between those 2 solutions and their respective drawbacks... until I found an amazing very simple solution reading between the lines of the (excellent) 
[DragonFly documentation](http://markevans.github.com/dragonfly/) : the "to_file" method ! It only took me a couple of hours to write this helper that ensure the file exists on the filesystem, and only if not, call DragonFly to handle the resize and cache the thumbnail where it is expected to be. Everything is done at the view level, and the helper can also take any argument you would want to see in an img tag (yes, data attributes too).

'Want some examples ?

# HAML template
= thumbnail_tag user.avatar, '100x100'

# client side HTML
<img src='/images/user_avatar.jpg' width='100px' height='100px' alt="user_avatar" />
More tricky

# HAML template
= thumbnail_tag product.image, '200x50', :alt => "such a nice product name", :data => {:do =>'some_action', :trigger =>'that'}

# client side HTML
<img src='/products/small/product_image_file_name.jpg' width='200px' height='50px' alt="such a nice product name" data-do='some_action' data-trigger='that' />
You will find all code, tests, installation instructions and usage on the 
[github repo](https://github.com/gbarillot/dragonfly_helper).
