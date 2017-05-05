---
title: Gérer correctement les accents avec Ruby, Rails et upcase
date: '2012-08-14'
layout: post
tags:
- ruby-on-rails
---

C'est assez étonnant d'avoir encore ce genre de problème de nos jours, mais Ruby (même 1.9.3), ne gère toujours pas correctement les passages de caractères accentués en majuscule. Explication :> puts "café".upcase
CAFé
Pas terrible, hein ? Une solution est d'utiliser la Gem 
[unicode_utils](http://unicode-utils.rubyforge.org/) et de surcharger la class String pour pouvoir l'utiliser de façon transparente.

Commencez par install la Gem en l'ajoutant au Gemfile puis bundle install (comme d'habitude)

Ensuite, créez le fichier suivant :

require "unicode_utils/upcase"

class String

  def upcase
    UnicodeUtils.upcase(self)
  end

end
Sauvegardez le tout dans "/config/initializers/string_upcase_patch.rb"

Voila, c'est tout. Maintenant, quand vous faites un upcase sur une chaine contenant des caractères accentués, vous avez bien :

"café".upcase
#=> CAFÉ
Espérons que tout ça sera prochainement intégré directement dans Ruby
