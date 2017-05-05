---
title: PDF Generation using Ruby is just a f**** pain
date: '2010-10-05'
layout: post
tags:
- ruby-on-rails
---

It's been now 20 hours I'm working on a PDF invoice document. Man... 20 hours for a fu**** stupid invoice !!! I am very surprised about the lack of _real_ good solutions. Here's what I have to deal with by now :


[PDF-Writer](http://ruby-pdf.rubyforge.org/pdf-writer/) : Well documented grand father I already used, but does not handle PNG transparency, nor UTF-8 (WTF ?!)


[Prince](http://www.princexml.com/) : Looks nice but... 3 800 $ per server Licence !!!


[HTMLDOC](http://htmldoc.rubyforge.org/) : Absolutly not railysh. Have to turn around again and again to make it work (the ugly way)


[Simple ruby PDF Generator](http://www.railslodge.com/plugins/860-simple-ruby-pdf-generator) : Yeah... simple


[PDFKit](http://thinkrelevance.com/blog/2010/06/15/rethinking-pdf-creation-in-ruby.html) : Promising idea, but I can't get it to work the "Rails way" using Rack on my box (Rails 2.3.8). Documentation near level 0, and very new kid on the block. Later, maybe ?!


[Ruby FPDF](http://zeropluszero.com/software/fpdf/) : Ruby port of PHP's FPDF lib. I didn't love the original FPDF very much in my PHP years... plus for this ruby port : No documentation at all, no Github repo, very few users, last update two years ago. I don't feel really confident about it. I maybe wrong.


[Prawn](http://prawn.majesticseacreature.com/) +
[prawnto](http://www.cracklabs.com/prawnto) : Fast, efficient pure Ruby lib, and "working the Rails way" using the prawnto plugin. On the other hand : the very bad news about Prawn is its DSL Syntax which is absolutly horrible. Nevermind, read the doc ! And here's the second bad news : I've never ever ever, seen such a confusing Documentation in ten years of programing. Examples given on Github work sometimes (and sometimes... not), official Doc is lacking, althought I've found at least 3
[differents](http://rdoc.ryanstenhouse.eu/prawn-graph/)
[docs](http://prawn.majesticseacreature.com/docs/0.8.4/prawn-core/)
[sources](http://rdoc.rubyforge.org/RDoc.html).  Maybe a real good unified and up-to-date documentation should be enough to really understand and use Prawn, but by now, here I am : 20 hours of tough work just to render a simple invoice. Damn !...

If you really (I mean : REALLY) have to generate PDF, I would say... no forget about it, don't use PDF in your rails app. Or wait 2/3 years Prawn to have a decent doc and tutorials.

 
