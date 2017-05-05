---
title: 'SIPS/ATOS et Ruby on Rails avec le plugin ''atos'' '
date: '2011-03-31'
layout: post
tags:
- ruby-on-rails
---

Après
[Paybox](/blog/fr/2010/11/30/209-dialoguer-facilement-avec-les-serveurs-de-paiement-paybox-depuis-rails), je me suis dernièrement interessé à SIPS/ATOS, poids lourd du paiement ligne hexagonal. Derrière une apparente complexité, le principe est en fait assez simple :*L'acheteur valide son panier, un controller récupère les paramètres (prix, id du panier...), les envoie dans un binaire qui crypte le tout et renvoie un formulaire HTML avec 3 (ou +) logos de carte de crédit au sein du site marchand


*L'acheteur choisi la carte de crédit appropriée et part sur le site de la banque


*Une fois les numéros de carte validés sur le site de la banque, celui-ci répond au marchand "dans le dos du navigateur" (c'est l'auto-response) via une chaine cryptée


*un controller récupère l'auto response et la passe à nouveau dans un binaire afin d'en obtenir un tableau associatif
Ne trouvant rien de simple qui me convienne, j'ai codé un petit plugin qui permet de faire tout ça dans Rails très facilement. Dans une console à la racine de votre appli :

script/plugin install git@github.com:gbarillot/atos.git
Ensuite, déposez les fichiers fournis par la banque dans /lib/atos. Le répertoire lib doit ressembler à ça :

/mon_appli
  /lib
    /atos
      /bin
request
request_2.4.18_2.96
....
      /param
certif.fr.014295303911111
parmcom.014295303911111
parmcom.sherlocks
pathfile
Petites remarques : le numéro "014295303911111" en suffixe correspond au marchant_id de test, et "sherlocks" correspond au fait que je passe par LCL. Si vous passez par la Société Générale, vous aurez "parmcom.sogenactif". Je préfère vraiment le "conventions over configuration", mais vous pouvez aussi passer les chemins vers vos fichiers au niveau de l'instanciation de la classe Atos. Ca rajoute juste une étape :

atos = Atos.new(
  :root_dir=>'/path/to/your/main/dir'
)
.... et ensuite :
@request = atos.request(
  :merchant_id=>'014295303911111',
  :amount=>'1500',
  :customer_id=>session[:customer_id],
  :automatic_response_url=>"http://mon_site.com/payment/validate",
  :normal_return_url=>"http://mon_site.com/payment/fr/confirm",
  :cancel_return_url=>"http://mon_site.com"
)
Tant que nous sommes dans le paramétrage des fichiers, déposez aussi le répertoire "logos" et contenant les logos des cartes dans un répertoire public de votre appli (par exemple /public/images/logos). Prenez aussi soin de renseigner le fichier "/lib/atos/param/pathfile" avec tous les chemins
 vers les différents répertoires que nous venons de créer

Ok, maintenant que tout est en place, on va pouvoir commencer à faire tourner tout ça. Récuperez l'action de l'acheteur lorsqu'il valide son panier via l'URL de votre choix, et générons la requête. Depuis le controller :

@request = Atos.new.request(
  :merchant_id=>'014295303911111',
  :amount=>'1500',
  :customer_id=>session[:customer_id],
  :automatic_response_url=>"http://mon_site.com/payment/validate",
  :normal_return_url=>"http://mon_site.com/payment/fr/confirm",
  :cancel_return_url=>"http://mon_site.com"
)

render :template=>'payment/call_request'
Si tout se passe bien, nous récupérons dans @request un formulaire HTML avec les logos des cartes, ainsi qu'une variable "DATA" dans un champ "hidden" contenant l'intégralité de notre requête cryptée, il n'y a plus qu'à l'afficher dans le template (ici avec HAML) :

%span
  = "Sélectionnez votre type de carte :"
%br
= @request
------------ L'acheteur clic sur un des logos de carte et se rend sur le site de la banque. Celle-ci va maintenant nous répondre ---------------------

On récupère l'auto-response sur une URL à l'écoute en POST (je vous laisse créer la route de votre choix, dans mon exemple, c'est /payement/fr/validate). Il n'y a que 2 lignes à ajouter dans le controller approprié :

response = Atos.new.response(datas)

response[:response_code] # 00 => transaction réussie
...
Et hop, on obtiens un joli Hash avec toutes les variables de réponse disponibles dans l'API (voir le "dictionnaire des données" fourni avec l'API pour tous les détails). Maintenant, à vous de traiter cette réponse selon que le paiement a été accepté ou refusé, puis de valider l'achat dans la Base...

 

Quelques petits détails :

*les 6 paramètres que j'utilise dans mon exemple au niveau de la requête sont les seuls à être requis par le plugin, mais vous pouvez tout à fait envoyer tous les paramètres stipulés dans le "dictionnaire des données", rajoutez simplement les couples "clef/valeur" dans le hash de la requête.


*Par défaut la langue et la devise utilisés sont "fr/euro", mais vous pouvez surcharger avec ceux de votre choix au moment de l'instanciation de la classe Atos.


*Les URL de retour (normal/cancel) sont envoyées par POST, n'oubliez donc pas d'écouter aussi en POST les routes correspondantes


*C'est idiot mais ne pas oublier de lever la protection CSRF pour l'auto response (par rapport à mon exemple, ce serait "protect_from_forgery :except=>:validate"). Sans quoi l'auto-response ne sera jamais recevable par votre controller.
