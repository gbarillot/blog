---
title: 'RubyPants : Le Saint Graal de l’apostrophe et du Guillemet'
date: '2009-09-21'
layout: post
tags:
- ruby-on-rails
---

Bien prendre en charge les guillemets et autres apostrophes situé dans le contenu d’un site est un truc qui n’a vraiment l’air de rien, semble parfaitement naturel, et qui peut pourtant -en tant que développeur- vous rendre complétement dingue ! En effet : tout language de programmation utilise
lui aussi, ces mêmes guillemets et apostrophes, et bien souvent “language de programmation” et “phrase entre guilletmets” se chevauchent et s’entremêlent finement. Si en plus, vous avez un minimum d’élégance et que vous utilisez de beaux guillemets différents pour la gauche (“) et la droite (”), le problème prend rapidement de l’épaisseur.

Après des années de bricolage en PHP, j’ai ENFIN trouvé une solution avec Ruby, robuste et diablement efficace :
[RubyPants](http://kronavita.de/chris/data/rubypants.rb)

La documentation étant inexistante, je me fends d’un micro tuto, adapté à Rails :

Placez le fichier RubyPants.rb dans le répertoire /lib

Dans le controller contenant votre insertion de contenu dans la BDD, ajoutez tout en haut :require ’RubyPants’
Dans la méthode qui doit insérer le contenu, instanciez votre classe avec votre chaine en argument :

my_string = RubyPants.new(’Ceci est une phrase “entre guillemets“)
Et voila ! Maintenant, si vous appellez votre chaine de caractère avec la méthode “to_html“, vous obtenez :

my_string.to_html => Ceci est une phrase “entre guillemets”
