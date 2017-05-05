---
title: Installer Ruby on Rails chez OVH en 5mn chrono
date: '2009-07-20'
layout: post
tags:
- linux
- ruby-on-rails
---

Vous avez un serveur dédié (RPS dans mon cas) sous Ubuntu (je suppose que c’est pareil pour Debian), et vous avez envie d’y installer Ruby on Rails ? Bonne idée ! D’autant que c’est vraiment pas compliqué

Tout d’abord, fuyez les versions installées via apt-get et faites un apt-get remove –purge de tout ce qui peut concerner ROR de près ou de loin. Maintenant, pour TOUT ce qui va suivre, restez en Root.

# On commence par n’installer “que” Ruby (ce sera notre seule et unique utilisation d’apt) avec :apt-get install ruby-full
#Ensuite,
[télechargez ruby-gems depuis ruby forge](http://rubyforge.org/frs/?group_id=126) et SURTOUT, NE VOUS SERVEZ PAS DE LA VERSION APT, où alors, c’est que vous avez vraiment envie de vous amuser 4/5 heures avec des problèmes de dépendance (je sais de quoi je parle…). Ensuite comme d’hab :

tar zxvf rubygems-1.3.4.tgz
Faites bien l’extraction du Tar.gz en Root, il pourait y avoir des problèmes de droits ultérieurs.

#Installez maintenant Ruby-gems :

cd rubygems-1.3.4.tgz
ruby setup.rb
Chez moi (en local et sur le serveur), j’ai un warning à la fin à cause d’une doc non trouvée : on s’en fout. Une fois l’install terminée, vous pouvez aussi supprimer l’archive tar.gz ainsi que le répertoire “rubygems-1.3.4” qui va avec.
Bien, maintenant, chose étrange, si vous tentez tout de suite de faire un

gem install rails
Vous allez vous retrouver avec un assez effrayant “commande introuvable“. Pas de panique, c’est juste que la commande “gem” s’appelle dans un shell avec “/usr/bin/gem1.8“.

# Créez un alias dans votre .bashrc

alias gem = /usr/bin/gem1.8
Vous y êtes !

gem install rails
5 petites minutes à attendre… et vous voila avec une version 2.3.2 tout neuve et clinquante.

#Il ne reste plus qu’à installer Passenger pour faire tourner tout ça dans Apache2 :

gem install passenger
passenger-install-apache2-module
#Sans oublier RMagick pour manipuler des images tant que nous y sommes :

 

gem install rmagick
Rien de compliqué, en fait, le truc c’est de :
- ne pas utiliser Apt en dehors de l’install de Ruby
- bien télécharger ruby-gems depuis Ruby forge
- ne pas trop être surpris par le “commande introuvable” après l’install de Rub-gems
