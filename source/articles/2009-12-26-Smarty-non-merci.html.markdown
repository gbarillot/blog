---
title: Smarty, non merci
date: '2009-12-26'
layout: post
tags:
- php
---

Ca fait maintenant plusieurs jours que je travail sur un E-Commerce Prestashop avec un thème et des fonctionnalités bien tordues. Mais bon, Prestashop est une bonne plateforme, bien concue. Créer un module ou tordre un peu le Core pour l’adapter à ses fins est assez facile. Par contre, le problème, c’est ce p*** de SMARTY !!! Je me demanderai toujours pourquoi, mais pourquoi donc les gros projets (sauf Magento, tiens…) ne peuvent s’empêcher de s’embarquer dans ce bidule qui, pêle-mêle :*Ne simplifie pas _du tout_ la vie du développeur


*Ne simplifie pas non plus le job du Designer


*Alourdi considérablement l’execution du code


*Ne sépare EN RIEN le business logic du template


*Rend très vite les templates tout simplement illisible
 

Alors quoi ? I18n ? YAML permet de faire plus clair, concis et tout aussi efficace. Séparation de la logique du template ? Je vois pas le rapport, MVC est là pour ça, et c’est pas de rajouter une deuxieme couche au niveau de la vue qui va arranger quoi que ce soit. Quant à la lisibilité du template, je vous renvoie vers
[HAML](http://haml-lang.com/), et vous verrez -si vous ne connaissez pas encore- ce que “lisibilité” veut dire !

Bref, Smarty, non merci.

 

Edit : ha tiens, je ne suis
[apparemment pas le seul.](http://www.codeassembly.com/Why-template-systems-like-smarty-are-useless-and-sometimes-bad/)
