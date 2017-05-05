---
title: Automatiser des taches récurentes avec Rails
date: '2011-02-23'
layout: post
tags:
- ruby-on-rails
---

Il existe plusieurs façons d'effectuer des taches récurentes au sein d'une application Rails, notamment avec Rake. La technique que j'utilise présente comme (seul ?) inconvénient d'être un peu lourde puisque elle relance le stack complet lors de son appel. Bon, d'un autre côté, je m'en sert principalement pour les backups et les envois de Mails nocturnes, alors les perfs, dans ce cas, je m'en fout un peu. En revanche, cette technique présente le gros avantage de pouvoir bénéficier de tout Rails (ActiveRecord, ActiveMailer...), et permet aussi d'être intégré au sein de l'appli d'une manière que je trouve plutôt cohérente. Bon, assez parlé, on s'y met :

Créons un répertoire qui contiendra tous les "controllers" de nos tâches nocturnes, nous allons le placer à côté des models et des controllers, appelons le "shedulers"

 $ cd /home/mon_appli/app/
$ mkdir shedulers
$ ls
controllers
helpers
models
shedulers
views
Dans ce répertoire "schedulers", créons un fichier -par exemple- "newsletter.rb" (notez l'héritage d'ActiveRecord)

class Newsletter < ActiveRecord::Base

  this_time = Time.now

  accounts = Account.find(:all)

  accounts.each do |account|

    Notifier.deliver_email(account.email,"Newsletter du #{this_time.strftime('%d:%m:%Y')}")  

  end

end
Hop, vous bénéficiez d'ActiveRecord, vos relations et tout le toutim. Idem pour ActiveMailer, vous avez tout sous la main ! Maintenant, il ne reste plus qu'à appeler notre fichier grâce au script/runner de Rails. Placer vous à la racine de votre appli et taper dans la console :

script/runner app/shedulers/newsletter.rb >> log/production.log 2>&1
Ca marche ? Bon, ben maintenant c'est facile, y'a plus qu'à appeler cette même commande avec Cron

5 3 * * * cd /home/mon_appli && script/runner ./app/crawlers/debiter.rb >> /home/mon_appli/log/production.log 2>&1
Dans cet exemple, la newsletter partira donc chaque nuit à 3h05, et les erreurs éventuelles seront loguées dans le Log habituel de notre appli.
