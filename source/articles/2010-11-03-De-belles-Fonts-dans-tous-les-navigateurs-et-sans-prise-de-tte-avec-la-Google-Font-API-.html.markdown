---
title: 'De belles Fonts dans tous les navigateurs et sans prise de tête avec la Google
  Font API '
date: '2010-11-03'
layout: post
tags:
- la-technique
- les-gouts-et-les-couleurs
---

Depuis le temps qu'on doit se battre avec des images pour avoir un tant soit peu de variété au niveau des Fonts, c'est avec un vrai grand plaisir que j'ai d'abord accueilli les possibilitées ouvertes par CSS3 et l'attribut @font-face... hélas, je me suis rapidement retrouvé face aux différences d'implémentations entre navigateurs, avec des formats de fonts différents (TTF pour un peu tout le monde, et EOT pour IE), et des rendus plus ou moins approximatifs (étonnant, hein ?!).

Dans ce paysage, une solution devient alors très interessante :
[Google Font API](http://code.google.com/intl/fr/apis/webfonts/docs/technical_considerations.html). Le principe : vous incluez un bout de code, et Google se charge de vous envoyer la bonne font en fonction de votre navigateur. En prime, Google se charge du hosting et de la bande passante nécessaire à cette même font. Sympa, non ?

Un exemple en deux lignes<head>
...
<link href='http://fonts.googleapis.com/css?family=Yanone+Kaffeesatz:extralight' rel='stylesheet' type='text/css'>
...
</head>

<body>
<h1 style='font-family:Yanone Kaffeesatz'>Foo Bar !<h1>
...
Ce qui nous donne à l'écran :


![google fonts API example](/cache/guillaume-barillot.com/images/170xauto/google_fonts_api.png)

Vous avez aussi la possibilité d'appeler l'API via Javascript (ce que je fais dans le projet sur lequel je suis), mais je vous laisse voir
[la doc](http://code.google.com/intl/fr/apis/webfonts/docs/technical_considerations.html) ainsi que les
[différentes Fonts actuellement disponibles.](http://code.google.com/webfonts/)
