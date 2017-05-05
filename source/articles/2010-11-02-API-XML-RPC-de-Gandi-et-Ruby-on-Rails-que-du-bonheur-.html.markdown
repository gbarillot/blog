---
title: 'API XML-RPC de Gandi et Ruby on Rails : que du bonheur !'
date: '2010-11-02'
layout: post
tags:
- ruby-on-rails
---

Après plusieurs semaines d'hésitation, de recherche et de prospection, je vais finalement utiliser les services de
[Gandi](http://www.gandi.net/) afin de gérer les noms de domaine du (gros) projet sur lequel je travail. Quatre raisons à cela :*Gandi est basé en France, avec un helpdesk Mail et/ou téléphone sur lequel on peut compter


*J'ai consulté et disséqué des dizaines d'offres revendeurs(worldwide). Finalement, Gandi n'est guère plus cher que les autres (pas le moins cher non plus... mais les différences se jouent à 2 ou 3 Euros près par an : pas de quoi prendre des risques en optant pour un Registrar exotique)


*Si vous me lisez couramment, vous savez que j'accorde une importance primordiale à la documentation, et celle de l'API XML-RPC est un modèle du genre :
[re-mar-quable](http://wiki.gandi.net/fr/api-xml/docs/domain)


*C'est assez dingue, parce que le besoin doit quand même pas être si courant que ça... mais Il existe un plugin Rails pour communiquer avec l'API ! Décidemment, comme je l'ai entendu lors du dernier apéro Rails à Lyon : "grâce aux plugins, on a plus rien à faire, tout est déja pré-existant, testé et validé". Ca se confirme.
Concrétement, je viens de faire mes premiers essais en production ce matin, et il ne faut pas plus de 20 lignes de codes pour se connecter à l'API, vérifier si un domaine est libre, si oui, le réserver, le verrouiller et spécifier les DNS. 20 lignes, commentaires compris ! Merci Gandi, merci Rails, merci
[Xavier](http://defrang.com/) pour ton plugin.
