---
title: Redimensionnez vos images à la volée avec Ruby on Rails
date: '2011-05-16'
layout: post
tags:
- ruby-on-rails
---

J'ai re-factorisé et modifié en profondeur la syntaxe d'appel de mon bon vieux plugin
[Thumbnailer](https://github.com/gbarillot/thumbnailer). Certes, vous pouvez déja redimensionner les images lors de l'Upload avec
[paperclip](https://github.com/thoughtbot/paperclip), mais thumbnailer vous permet d'aller encore plus loin :*Resize à la volé au niveau de la vue


*Calcul automatique des proportions


*Gestion automatique du cache, les images ne sont traitées qu'une seule fois par RMagick


*Possibilité d'appel en "remote", redimensionnez vos images depuis votre client en JS !
Niveau utilisation, on ne peut pas faire plus simple :

# View
<%= thumbnailer :src=>'/images/my_image.jpg', :width=>'200' %>
Et le plugin se charge tout seul de vous générer une image de 200 pixels de large, qui est mise en cache dans '/cache/images/200xauto/my_image.jpg'. La vue finale affichant un tag img comme celui-ci :

<img src='/cache/images/200xauto/my_image.jpg?1305495323' width='200' alt='my_image' />
Tous les attributs possibles d'une balise img sont reconnus, y compris les évenements JavaScript. L'attribut 'alt', si il n'est pas spécifié, sera automatiquement généré à partir du nom de fichier. Vous noterez aussi que le nom de fichier est suffixé par un timestamp, permettant au cache client side de gérer une image différente mais portant le même nom de fichier, tout comme le 'image_tag' original de Rails.

En bonus, avec le paramètre "remote", l'appel de l'image peut aussi se faire directement depuis le paramètre 'src' du tag img :

# View
<%= thumbnailer :src=>'/images/my_image.jpg', :width=>'200', :remote=>true %>

# Final output
<img src='/thumbnailer/200xauto/images/my_image.jpg' width='200' alt='my_image' />
Effet de bord sympathique, vous disposez maintenant d'une simple URL pour appeler une image de n'importe quelle dimension depuis votre client en Javascript, genre :

$('my_image').src='http://my_domain.com/thumbnailer/200xauto/images/my_image.jpg';
alert("Look ! The image has been resized !");
Ca fait maintenant 2 ans que j'utilise ces features dans tous mes projets. Au début c'était une collection de helpers, de routes et de controllers, puis j'ai pris un peu de temps pour packager tout ça dans un plugin. Je pense maintenant que cette nouvelle version est plus clean et efficace, mais je vous laisse vous faire votre avis là dessus. Comme d'habitude, si vous avez des remarques, laissez un commentaire...
