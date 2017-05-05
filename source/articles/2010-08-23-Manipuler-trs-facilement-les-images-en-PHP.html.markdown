---
title: Manipuler (très) facilement les images en PHP
date: '2010-08-23'
layout: post
tags:
- php
---

Je viens de découvrir ça :
[http://www.mawhorter.net/web-development/simple-image-manipulation-in-php-rotate-resize-crop-flip-and-mirror-thumbnails-square-and-regular](http://www.mawhorter.net/web-development/simple-image-manipulation-in-php-rotate-resize-crop-flip-and-mirror-thumbnails-square-and-regular) et de l'intégrer dans un projet Prestashop où j'ai besoin de manipuler facilement des PNG 24 bits semi-transparents.

Franchement, je n'ai qu'un mot à dire : chapeau. La syntaxe des appels aux différentes méthodes de la classe est très simple à assimiler, et ça fonctionne remarquablement bien. La grosse différence avec toutes les autres classes du même genre que j'ai pu essayer, c'est l'excellente gestion des fonds transparents sur les PNG (en fait, c'est très simple : vous n'avez pas à vous en préoccuper. Ca marche, et c'est tout.)
