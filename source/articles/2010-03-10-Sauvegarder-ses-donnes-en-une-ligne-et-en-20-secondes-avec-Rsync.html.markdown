---
title: Sauvegarder ses données en une ligne (et en 20 secondes) avec Rsync
date: '2010-03-10'
layout: post
tags:
- la-technique
- linux
---

Les sauvegardes, c’est vital ; et avoir à tout moment un backup récent est tout aussi crucial, qu’important et… négligé. Mais on ne peut raisonnablement pas re-copier l’intégralité de son serveur bien au chaud sur son PC par FTP ?! Cela ne prend rien moins qu’un temps monstreux, alors faire ça tous les jours… non, ce qui serait bien, c’est de ne télécharger QUE la différence entre deux sauvegardes. C’est là qu’intervient Rsync, qui va vous permettre d’effectuer ces sauvegardes incrémentielles. Le Net regorge de tutos tous plus complets les uns que les autres et que je vous encourage à lire pour votre culture personnelle. Ceci dit, si tout ce que vous voulez, c’est copier le /home de votre serveur dans le /home de votre PC, et que vous avez une Ubuntu sur un RPS chez OVH, je vais vous faire gagner du temps ; ouvrez un terminal et tapez cette ligne de commande en root :rsync -e ssh –delete –delete-excluded -avR votre_login_ssh@votre_machine.ovh.net:/home/ /home/mon_repertoire_de_sauvegarde
Voila, cherchez pas plus loin, c’est aussi simple que ça. La première sauvargarde va être énorme et vous prendre un temps fou (puisque c’est la première), mais ensuite vous n’échangerez plus que la différence ! Et hop, à vous les sauvegardes quotidiennes, et les bonnes nuits de sommeil.

 

 
