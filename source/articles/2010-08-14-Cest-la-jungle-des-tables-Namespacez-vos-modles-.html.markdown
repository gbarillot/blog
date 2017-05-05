---
title: C'est la jungle des tables ?! Namespacez vos modèles !
date: '2010-08-14'
layout: post
tags:
- ruby-on-rails
---

Au delà de ce titre quelque peu obscur, je viens de découvrir un truc super pratique avec Rails lorsque ça devient la jungle dans les modèles (le projet sur lequel je bosse en comprend pas moins de 72 sur deux BDD distinctes). En fait, il suffit de les répartir dans des sous dossiers, et de dire à Rails d'aller regarder dedans. Voui, c'est aussi simple que ça, pas besoin de renommer vos modèles, ou (pire) mettre vos classes dans des espaces de noms... Par exemple, travaillant sur deux bases à la fois, j'ai placé tous les modèles intervenant sur une des bases dans un sous répertoire "base_2". Il suffit ensuite d'indiquer à Rails de regarder dans le répertoire "base_2" :#/app/config/environment.rb

config.load_paths << "#{RAILS_ROOT}/app/models/base_2"
Je retrouve tout de suite un peu d'ordre dans cette grosse jungle que commençait à être "/app/models", et sans avoir besoin de renommer une quelconque classe.
