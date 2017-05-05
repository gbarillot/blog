---
title: Missing the Rails 2.3.5 gem. Please `gem install -v=2.3.5 rails` although
  Rails IS already installed
date: '2010-09-08'
layout: post
tags:
- ruby-on-rails
---

So it appears that Rails apps sometimes boot up strangely... I have a server properly configured that already runs about 5 rails applications, without any single issue ; but as I'm trying to install a copy of Fat Free CRM this morning, the server crashs and application boot fails with this weird message :>Missing the Rails 2.3.5 gem. Please `gem install -v=2.3.5 rails`, update your RAILS_GEM_VERSION setting in config/environment.rb for the Rails version you do have installed

I digged a little deeper into it and found that Rails startup is not very verbose nor curious at all : it simply throw out this message
whatever could be the error !!! In order to raise the real and specific error that crash you boot, you'll have to edit the /config/boot.rb file, and found these lines :

rescue Gem::LoadError => load_error
 $stderr.puts %(Missing the Rails #{version} gem. Please `gem install -v=#{version} rails`, update your RAILS_GEM_VERSION setting in config/environment.rb for the Rails version you do have installed, or comment out RAILS_GEM_VERSION to use the latest version installed.)
  exit 1
end
Now, add this at the beginning of the rescue block : raise load_error.inspect . This should throw out the real and usable error message.
