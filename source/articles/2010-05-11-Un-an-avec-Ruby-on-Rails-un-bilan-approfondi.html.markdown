---
title: 'Un an avec Ruby on Rails : un bilan approfondi'
date: '2010-05-11'
layout: post
tags:
- les-gouts-et-les-couleurs
- ruby-on-rails
---

Celà fait maintenant un an (et une ‘tite quinzaine de jours…) que j’ai découvert Ruby on Rails, et le moment me semble idéal pour faire un vrai bon bilan en profondeur de cette année de travail. Je serais d’abord direct, clair et concis, avant de m’étendre un peu plus dans la conclusion.


**# Ce qui est très bien :**


- La documentation : oui, je commence directement par ce point, qui me semble es-sen-tiel, et où Rails est tout simplement époustouflant. Grâce à un travail rien moins que
[monumental](http://api.rubyonrails.org/) de documentation et de
[vulgarisation](http://guides.rubyonrails.org/), la courbe d’apprentissage est remarquablement courte, et se passe vraiment bien.

- Ruby : au début, je me tournais plutôt vers les Framework PHP genre Cake ou Symphony, par peur d’apprendre encore un nouveau language. En fait, c’est bien le contraire qui s’est passé : j’ai très très vite appris à me débrouiller avec Ruby et tout aussi vite oublié PHP (non, résister à la tentation, ne pas dire du mal des vieux languages plein de rustines… hem…)

- MVC : Modèle, Vue, Controleur. Heuuu, “what else” ?

- RJS : Ajax, en plus d’accélérer les applications (pas besoin de recharger toute la page), apporte un côté ‘bling bling’ dont tous les clients raffolent. Le seul truc, c’est que c’est un peu long et parfois bien tordu à concevoir sans Framework. Avec Rails, les RJS et Prototype, badaboum… on en vient presque à oublier qu’on fait de l’AJAX tellement c’est simple et vite mis en place.

- REST : la façon dont sont implémenté les routes, l’URL rewriting et les interactions avec les controlleurs sont tout simplement gén-iales. Avec RESTfull routing, les adresses sont claires (et courtes !) et vous savez tout de suite ou vous emmène chaque URL.

- I18n : L’internationalisation d’une appli peut vite devenir laborieuse. Aucun souci ici, tout est prévu depuis le départ pour vous simplifier la tâche. Dates, heures, expressions, requêtes… il suffit de respecter une poignée de convention et le Framework s’occupe de toutes vos traductions. Trop pratique !


**# Ce qui est bien :**


- La souplesse : voila bien un argument contre Rails que j’ai souvent pu lire : “tu es obligé de nommer tes tables d’une certaine façon” ou encore “je veux appeler mes clés étrangères autrement que ‘foreignkey_id’” et autres aneries… En fait, Rails vous pousse juste à utiliser quelques conventions simples afin de vous faire gagner un MAX de temps. Si vous voulez _vraiment_ faire autrement, ou tout simplement que vous devez reprendre un projet existant, il sera toujours extremement simple d’adapter vos propres conventions au sein du Framework. Vous n’avez vraiment aucun souci à vous faire, Rails n’est absolument pas psycho-rigide !

- Active Record : comment parler de Rails sans Active Record ??! Fini les tableaux à 153 dimensions de PHP et le XML des ORM de J2EE. Avec ActiveRecord, tout devient objet, et ridiculement simple à manipuler. Tout simplement génial.

-
[HAML](http://haml-lang.com/) : alors ça c’est un effet de bord assez inattendu. Découvert par hasard avec le plus grand des dubitatismes (ne me parlez pas de Smarty et autre PHP template…), j’ai finalement adopté sans aucune réserve ce language de template. Je retrouve enfin la lisibilité de Python, même avec des mises en pages franchement complexes bourrées d’AJAX, le template reste clair et limpide. Comme tout ce qui tourne autour de Rails, le temps d’apprentissage est ultra court, et l’essayer c’est l’adopter ! Note : il parait qu’il existe des bindings pour PHP, à voir…


**# Ce qui est moins bien :**


- Mauvais cross platform. Oui, il existe bien un genre de Wamp/EasyPHP pour Windows (
[Instant Rails](http://instantrails.rubyforge.org/wiki/wiki.pl)), qui est très pratique pour découvrir Rails et faire ses premiers pas, mais on en trouve très-très vite les limites. Si vous voulez éviter toute surprise dans le déploiement de votre appli, et souhaitez profiter pleinement d’un environnement serveur puissant et souple, il vous faut une base Unix. Mac ou Linux ou BSD ou ce que vous voulez, mais pas Windows.

- L’hébergement : le mutualisé avec Rails, ça n’existe pas. Ou alors, c’est pas terrible et de toute façon toujours trop cher. Pour disposer d’une plateforme fiable et sérieuse, vous devrez obligatoirement vous acquitter d’au moins une quarantaine d’euros/mois pour un VPS, et vous taper l’install à la mano qui va avec. Si vous ne connaissez rien à la maintenance d’un serveur dédié sous Linux, ça va être le moment de vous y mettre…

- C’est lent. (soupir…) j’aurais tellement aimé vous dire que c’est faux, mais, malheureusement : non. C’est lent. Bon, ‘faut toujours comparer ce qui est comparable, c’est
[ni plus ni moins lent qu’un autre Framework](http://avnetlabs.com/php/php-framework-comparison-benchmarks) et face à Cake ou Django, on est dans les clous, ni mieux ni pire. Par contre, ne pas perdre de vue qu’il va falloir oublier les hébergement à 50 Euros/an tournant avec 512 Mo de RAM. Ceci étant, les fonctionnalitées de cache sont vraiment rapides et diablement efficaces à déploier. Pour peu que votre appli ne soit pas trop exigeante en terme d’interactivité, au final, il y a la possibilité d’égaler les perfs d’une page HTML statique (si, si…)


**# En conclusion :**



**Rails est parfait si :**


- Vous voulez proposer rapidement une appli type SaaS et vous disposez de ressources hyper limitées. Ce qui était d’ailleurs exactement le cas de figure lorsque DHH a créé le Framework, et qui est aussi mon cas.


**Rails est très bien si :**


- Vous cherchez une nouvelle techno pour remplacer le socle de travail de base de votre entreprise. Puissant, structurant, avec un environnement de tests unitaires, I18n, Open Source… J’entends et lis souvent que Rails est le futur “J2EE Killer”. Vous voulez mon avis ? C’est très probablement vrai.

- Vous avez toutes les casquettes et cherchez un couteau suisse pour des développements Web vite-faits/bien-faits dans des projets courts et “one-shot”.


**Rails ne répond pas à vos besoins si :**


- Votre but est de gagner rapidement de l’argent en répondant à un besoin ultra courant
**.**
Typiquement : du E-Commerce ou du site vitrine à la chaine. Dans ce cas, restez avec Joomla ou Wordpress et ne vous embarquez pas dans de longs et couteux développements sur-mesure, ça ne sert vraiment à rien de chercher midi à 14 heures (sauf pour la beauté du geste, bien sur, mais j’ai dit “gagner de l’argent”, et pas “se faire plaisir”. Ceci dit, à vous de voir…).

Voila pour ce bilan, j’espère vous avoir donné envie de découvrir ce merveilleux environnement de travail, qui ne cesse de m’impressionner par son côté pragmatique, et qui me permet de coder 3 à 4 fois plus vite qu’en PHP. Ce qui était avant hors de porté pour un developpeur seul est devenu tout à fait possible, et je peux désormais me concentrer pleinement sur le fond : le Design, l'interactivité des interfaces et les aspects métiers de chaque application.
