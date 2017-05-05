---
title: La meilleure façon (et la moins chère) de faire des screencasts au format flash
date: '2011-01-13'
layout: post
tags:
- la-technique
- les-gouts-et-les-couleurs
---

Cela m'aura finalement pris pas loin d'une journée avant d'arriver à une qualité optimale, mais il était vraiment important pour moi de réaliser des screencasts de bonne qualité afin de créer des rubriques d'aides dans mon prochain projet.

Durant cette journée de test, j'ai pu tester les solutions suivantes, pêle-mêle :*(Linux) Istanbul : plante régulièrement, et qualité d'image pas top


*(Linux) XVidCap : sympa, agréable, mais capture vidéo pas encore optimale


*(Linux) RecordMyDesktop : trop gourmand en resources


*(Linux) OpenshopvideoEditor : plante beaucoup trop régulièrement, inutilisable


*(Linux) Kdenlive : extrement gourmand en ressources et plante tout-le-temps (peut être lié au fait que je n'utilise pas KDE ?!)


*(Windows) Camtasia : Hem, 320$ la license, quand même ! Belle application, mais je ne trouve pas l'ergonomie phénoménale et les fonctionnalités sont somme toutes limitées (en démo du moins, mais ça ne m'a pas vraiment donné envie d'acheter la version payante)


*(Windows) Wink : Fonctionnalitées plutôt limitées, mouais, bof...


*(Windows) Super : arf, le nom d'appli le plus bidon que j'ai jamais vu !!! Bref, pour être sérieux, splendide usine à gaz permettant en théorie de transcoder n'importe quel type de média vers n'importe quel autre type (mov -> avi, mpg -> flv ...), et qui au final vous prend énormément de temps à paramétrer pour un résultat approximatif. Certainement extremement puissant, mais moi, mon but, c'est pas de pouvoir tout faire. Non, je veux juste passer de l'avi vers du flv avec la meilleur qualité possible. Point barre.
Finalement, j'ai trouvé le compromis idéal en utilisant 3 applis :

*Capturer l'écran avec CamStudio, en utilisant le codec "Techsmith" (éditeur de Camtasia ndlr) avec une sortie en AVI : qualité d'image vraiment irréprochable


*Monter sa vidéo, couper/coller / ajouter des titres... avec Windows Movie Maker : gratuit, hyper simple d'utilisation et présentant de très nombreux presets d'effets. Seul (tout petit) regret, le paramétrage de la vitesse de lecture : on a juste la possibilité de faire 2x plus rapide, point. Accélerer de 75% une fraction de film est donc impossible. Je peux me tromper, mais en tout cas jusque là, j'ai pas trouvé comment faire. Quoiqu'il en soit, je ne m'attendais sincérement pas à ce qu'il soit aussi facile de monter une vidéo, synchroniser de l'audio, rajouter des titres... bravo Microsoft (notez le, je ne le dis pas tous les jours !)


*Transcoder la vidéo avec WinFF : bon, dans le fond, c'est toujours du FFMPEG (tout comme Super), mais il y a dans cette GUI en surcouche quelques presets permettant d'encoder en FLV avec une excellente qualité. Ceci dit, il est toujours possible d'utiliser FFMPEG en ligne de commande avec les bonnes options (bon courage, vous n'avez pas fini de tatonner ;-)
Voila, si ça peut vous éviter de perdre votre temps comme j'ai pu le faire, ce petit billet aura rempli son rôle. Désolé de certaines critiques peut être un peu rapides, mais je n'avais pas le temps de rentrer dans les configurations de chaque appli et tout optimiser, ce qui aurait peut être changé mon point de vue sur certains avis. Au final, ce qui ressort ici est juste le résultat d'une journée de tatonnement à la recherche (rapide) d'efficacité. Ne m'en voulez donc pas d'avoir fait l'impasse sur certaines solutions (Camtasia notamment, qui semble bon leader dans ce marché).
