---
title: How to to make Vim to look like Atom
date: 2017-06-09 15:23 UTC
layout: post
tags:
- vim
---

## Why, and who is this for?

I love Atom. Really. Nonetheless, it has the bad habit to turn my 8G RAM MacBook into a big lazy slug.
Moving back to Sublime text is not really a good idea, since I'm a bit afraid of its future, at least for the V2 licence I bought about 6 years ago, and I have no plan
to buy a new licence for the V3.

So... what's left? I need a simple/dumb editor (no autocomplete all the way and code introspection), FAST and cross-platform.
Open Source should be mandatory too. Ideally, it could be great if I could learn to use a tool that I would not have to abandon in a few years, like I did with all
my previous editors. Then I saw [Fabien Cazenave](https://twitter.com/fabi1cazenave?lang=fr) using Vim in a workshop, it started to feel a _little bit_ less scary, and I decided to give it a try.

If you're an hardcore Vim user, you can pass your way. No, I didn't deactivate the mouse, no I do still use the arrow keys and I'm
really happy with it. Now, if you're like me a few weeks ago, more or less at the ":wq" level, and start struggling each time you have to
comment a 4 lines block in one shot, this blog post may put some light on what's possible with Vim.
Do no longer be afraid: with a good config file, a few tips and tricks and the help of some plugins, it can be <del>easy</del> accessible.


## 0. Short demo
Vim can be way more sexy than what you'd expect  
<br />
<video width="100%" controls>
  <source src="https://s3.amazonaws.com/gbarillot-blog/vim_custom.mp4" type="video/mp4">
</video>
<br />
## 1. Make sure your terminal accepts true colors rendering

Come one, we're in 2017, why should we stay stuck with those ugly 256 colors display?!
As a Mac user, I only had to download and install [iTerm2](https://www.iterm2.com/downloads.html). It automatically detected I was using ZSH and installation was a breeze.
If you're using Linux, you may have a look at [this page](https://gist.github.com/XVilka/8346728).


## 2. Download and install powerline fonts

Since we'll be using Airline (a plugin) to show up additionnal infos like the current mode, Git Branch... we'll need some patched fonts so Vim could display chars that are usually inexistent. This one should be simple too, just go [here](https://github.com/powerline/fonts), download the fonts and install them on your system.
If you stick to my Vim config file, actually, you should only have to install "Deja Vu Sans".


## 3. Backup your original vim config and files

(cause if you don't have a backup, don't change nothing ™)

```shell
  mv ~/.vimrc /some_backup_dir/.vimrc
  mv ~/.vim /some_backup_dir/.vim
```


## 4. Download the main Vim config

```shell
  cd ~ && git clone https://github.com/gbarillot/vimrc && mv vimrc .vimrc
```

## 5. Install all plugins

Plug is the only Plugin manager I used. Go [install it](https://github.com/junegunn/vim-plug), and once done, 
let's open up our config file:

```shell
  vim .vimrc
```

Now, type ":" (you should see the colon character appearing at the bottom left of the screen), followed by "PlugInstall".
If everything goes fine, you should see the screen split in 2, with download and installations status on the left.

## 6. Enjoy!

All plugins are correctly installed? Great, close the current file (the legendary "Escape :wq"), and re-open up Vim with one of your
project.... Done? Ok, now, take your time and read the next few lines to grasp how we can actually use it.  

<br />
## How the F§#&* do I use this now?!    
<br />
## The basics  
**[escape**] : go back to normal mode (you know, this NOT so normal mode where nothing appears when you type)  
**[escape i**] : enter insert mode, what you type is what appears on the screen  
**[escape v]** : enter visual mode, you can visually select sections of code, both vertically and horizontally  
**[y]** : "Yank", aka "Copy"  
**[x]** : eXterminate, delete current selection, weither it's a line, a char or a block  
**[p]** : wow, finally some command that makes sens : "Paste"

<br />
### Essentials
**$**  : get to the end of line  
**[shift] 0** : get to start of line  
**dd** : delete current line  
**yy** : copy the whole current line  
**u** : Undo last action  
**.**: (dot), repeat last action  
**o** : append a new line below and get into insert mode  
**O** : same, but this time line is inserted above the current line  
**:e js/newfile.js** : open a new file in js directory, and get ready to work on it

<br />
### Searching
Search for all files containing the word "users" anywhere in the app directory, recursively:

**:vimgrep users app/** **

Search for all occurences of "users" in the current file :

**/users**

... ant then just press * go to the next occurence of "users" 


<br />
### Some of the cool things you get with this config
**[Control f]** : Toggle the NERDTree file explorer on the left  
**[Control o] / [Control p]** : Go one buffer (== tab on Atom) to the left / one buffer to the right  
**[Control s]** : Save. Cause I don't know about you, but spreading my fingers all across the keyboard for "Escape : w" always sounded weird to me  
**[Control q]** : Quit. Close the tab you're in (ok, buffer with this Vim config), without closing the whole Vim session  
**[Control k]** : Toggle Komments. Comment/uncomment a line or a whole block

**Plus...**

+ copy/paste uses sytem buffer by default, so you can copy/paste from your browser directly into Vim, and the reverse
+ search results automatically open up in a new splited window
+ Swap files are not created (note that this could be seen [as a bad idea](https://news.ycombinator.com/item?id=1688068)... personnaly, not a problem)
+ Syntax highlighting for most common languages: Ruby, PHP, HTML, (S)CSS... and also HAML, Coffeescript, Pug (jade) and Vue
+ Autocompletion (using [Supertab](https://github.com/ervandew/supertab]))
+ Auto closing quotes, brackets...
+ Basic auto indent + landmarks for indentation levels    
+ You can still use the arrow keys
+ The mouse is usable (though you may consider visual mode, most of the time)


### And now the big question...

So, am I more productive now?! Well... No ;-). I'd say, probably, something about 5%-10% less productive. That's why I still use Atom at work, unless I need to do 
multiple CPU/RAM intensive tasks at the same time on my machine. On the other hand, I have to admit that, most of the time, I'm already more productive as long
 as I stay in the same file. I just waste a bit more time when I have to move/duplicate/rename files within a project, and "search in files" results are also a bit less easy to read and use, IMHO.  

All in all, I think it's just a question of time before I really get used to Vim usage, and that's why I'm now using it on my pet projects. I see it as an investment, and
 as we all know, an investment needs some time before it starts to pay back!



