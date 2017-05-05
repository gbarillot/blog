---
title: Un premier avis sur Spree (plateforme Ecommerce pour Ruby on Rails)
date: '2011-11-02'
layout: post
tags:
- ruby-on-rails
---

Depuis bientôt trois ans que je pratique quotidiennement Ruby on Rails, il est toujours resté pour moi une problématique encore non résolue : "et pour le E-Commerce, on fait comment ?". Je dois bien le dire, pour l'instant : "je fais comme je peux". En clair : Prestashop pour les grosses boutiques, et Rails maison pour les boutiques plus modestes mais avec des besoins très particuliers (produits sur mesures, système de promo. avancé...). Quoi qu'il en soit, la conclusion -à ce jour- n'a pas changé : IL FAUT UN MAGENTO EN RAILS.

J'ai bien essayé
[ForgeOS](http://www.forgeos.com/), en son temps, mais il s'est depuis perdu dans une plateforme beaucoup trop généraliste. Je cherche un sabre laser du E-Commerce, pas un couteau Suisse. Il y a eu aussi
[substruct](http://code.google.com/p/substruct/)... mais là encore, c'est plus "un CMS avec un panier" qu'autre chose, peu de monde semble d'ailleurs avoir suivi.

Nous voila donc fin 2011, et j'apprends que
[Spree](http://spreecommerce.com/) vient de lever 1,5 Million USD, le site Web est tout beau tout neuf et il semble y avoir une communauté derrière. Cool. J'essaye la demo en ligne... allez, je l'installe, et je vois ce qu'il y a dedans...*Rails 3.1.1, HAML, SASS/LESS, JQuery. On est vraiment dans ce qui se fait de mieux. En tout cas dans le mainstream de la communauté Rails


*55 tables dans la BDD... seulement ??! Pour situer, Prestashop est autour de 135 tables "out of the box", et Magento 218. Bon, ok, ça ne veut pas dire grand chose. Moui, mais bon... quand même, 55 tables, ça "tend quand même à signifier" que pas mal de features seront en add-on, ou bien tout simplement absentes par rapport aux deux autres poids lourds du secteur sus-nommés.


*Hooo, y'a une API ! Bon signe, ça prouve qu'on est proche des besoins des grosses boutiques.


*La doc. Ou plutôt : LA doc. Rien à redire concernant ce qu'on trouve sur le site, propre, net, précis (en Anglais, ça va de soit). Ok, mais _ailleurs_ ? Les tutos ? Les Blogs posts ?! Ben... pas grand chose. Quelques bribes éparses sur des forums, à prendre avec des pincettes tellement Spree semble avoir changé ces dernières
années mois. "On est dans le cutting edge, man !". En clair : va falloir s'accrocher.
L'installation se déroule facilement, puisque... toute l'application est contenue dans des Gems. Autant le dire franchement : je n'aime pas
 cette approche (que j'ai déja vu ailleurs :-/). Les Gems, à mon sens (et sauf erreur de ma part, j'ai lu DHH dire la même chose) sont là pour étendre des fonctionnalités, pas pour packager des applis. Perso, je ne suis vraiment pas fan de ce genre de chose, qui a vite tendance à ajouter de la "magie" (on ne sait plus où se fait quoi et comment). Concrétement, après installation, vous vous retrouvez donc avec une application... vide, puisque tout est dans des Gems.

Ok, bon, admettons, commençons à modifier une vue ou deux pour se mettre en jambes : que dit la doc ? Qu'il faut créer d'autres Gems pour y mettre sa customisation, même au niveau des simples vues :-/ Donc, si je suis bien tout ça : mon appli est, et restera vide. En fait, Spree, c'est un Framework de Gems, quoi... Plus sérieusement, je trouve que Spree est "une application Ruby qui utilise Rails", ce qui n'a rien à voir avec "une application Rails" classique dans laquelle on retrouve vite ses marques. Là, il va falloir suivre.

Là dessus, j'ai levé la tête du guidon et suis parti à la recherche de boutiques déja montées avec Spree : quelques "something went wrong" (si si) et quelques customisations de vues vraiment simplettes plus tard, j'ai décidé de laisser Spree dans un coin de mon /var/www, et d'y revenir dans quelques mois. Peut-être. Ou plutôt : j'espère.

Ce Post ne représente que ma modeste opinion après quelques heures de survol rapide de Spree. Si vous arrivez à me convaincre de m'accrocher encore un peu avec cette appli, libre à vous d'exposer vos arguments en commentaire, je n'attends que ça ;-)
