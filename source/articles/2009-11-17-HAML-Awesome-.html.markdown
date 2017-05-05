---
title: HAML ? Awesome !
date: '2009-11-17'
layout: post
tags:
- ruby-on-rails
---

Au hasard de mon bêta test de
[Forgeos Commerce](http://www.forgeos.com), je viens de découvrir
[HAML](http://haml-lang.com/about.html). Autant être clair, je n’ai jamais accroché à Smarty, et encore moins Phptemplate, ayant toujours trouvé que cela ne faisaist que rejouter une couche sans grand interêt (si ce n’est pour la localisation, moui, d’accord, bon…) par dessus un autre language de template qu’EST déja PHP. Et puis empiler des classes PHP sur d’autres classes PHP qui elles mêmes surchargent d’autres classes… à la fin ça se termine en Magento, bonjour l’usine à Gaz, et la facture du serveur dédié qu’il va falloir dimensionner en bête de course.

La dessus, est arrivé Rails et ses helpers, et les templates se sont vraiment épurés, commençant enfin à prendre tournure agréable, pragmatique et surtout : standardisées.

Mais alors, c’est quoi exactement là dedans HAML ??! Une façon rien moins que ré-vo-lu-tion-naire (si je vous le dis !) de gérer ses vues. Un language de templates de plus ? Non, LA solution !

Un petit exemple :


**HAML**#content
  .left.column
    %h2 Welcome to our site!
    %p= print_information
  .right.column
    = render :partial => "sidebar"
 


**=> HTML**


<div id="content">
  <div class="left column">
    <h2>Welcome to our site!</h2>
    <p><%= print_information %></p>
  </div>
  <div class="right column">
    <%= render :partial => "sidebar" %>
  </div>
</div>
Oui, c’est bien ça, l’indentation compte, et les classes CSS sont directement utilisées afin de définir les blocks ! Houuuuuulla, je sens que je vais être vite converti !
