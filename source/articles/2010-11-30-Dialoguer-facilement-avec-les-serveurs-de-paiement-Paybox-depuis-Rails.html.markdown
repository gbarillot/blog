---
title: Dialoguer facilement avec les serveurs de paiement Paybox depuis Rails
date: '2010-11-30'
layout: post
tags:
- la-technique
- ruby-on-rails
---

Décidement, les Railers Lyonnais font dans la monétique, ces temps ci... Après l'excelllllent
[plugin](https://github.com/lyonrb/payme) pour SIPS/Atos écrit par
[Damien Mathieu](http://dmathieu.com/fr) il y a peu, j'ai eu cette semaine à m'interfacer avec cet autre grand prestataire du paiement en ligne Hexagonal qu'est Paybox. A ce propos, juste un petit mot, parce que sans leur aide j'aurais eu du mal, mais la hotline de chez Paybox est remarquable : décroché en 1 sonnerie, réponses pertinentes, numéro non surtaxé... que du bonheur.

Bref, après une soirée à tourner autour de Net:HTTP sur du SSL, j'ai finalement codé une p'tite Class bien pratique pour dialoguer avec Paybox directement et en toute sécurité depuis vos controllers, vous pouvez la
[télécharger ici](http://www.guillaume-barillot.com/sites/guillaume-barillot.com/medias/files/103/paybox.rb).

Concrétement, l'utilisation est super simple : déposez le fichier paybox.rb dans vos modèles, puis il vous suffit d'instancier la classe de cette façon :# Controller
      response = Paybox.new(
:operation=>'00003',
:amount=>'1000',
:user_id=>'99',
:card_nbr=>'1234567891234567',
:expire=>'0311',
:cvv2=>'123'
      )
Nous effectuons ici une opération de type '00003' (demande d'autorisation + débit) de 1000 centimes sur notre abonné identifié par l'ID '99', titulaire de la carte '1234567891234567', avec la date de validité au 03/2011 et le code cvv2 '123'.

Maintenant, pour lire la réponse, c'est toujours aussi simple :

# Controller
response.coderesponse = '00000' #=> requete effectuée avec succès
# Ou bien encore :
response.commentaire = "PAYBOX : Numéro de porteur invalide" #=> Oooops, numéro de carte invalide
Et comme je suis vraiment gentil, j'ai même documenté tous les codes envois/retours de Paybox. Si tout se passe bien, vous n'avez même pas besoin de la doc officielle (au demeurant très bien faite). Bon, par contre, je ne sais pas écrire de commentaires ni de noms de variables autrement qu'en Anglais, et toute la doc (et les variables, WTF !) de Paybox sont en Français pur et dur, alors n'ayez pas peur du Mix Fran-glais...


**Edit**
 :
[Franck](http://twitter.com/#!/CesarioGW) a refactorisé et inséré tout ça (en mieux) dans un
[plugin](https://github.com/cesario/paybox) dispo sur Github.
