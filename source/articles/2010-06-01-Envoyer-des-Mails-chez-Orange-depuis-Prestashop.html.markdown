---
title: Envoyer des Mails chez Orange depuis Prestashop
date: '2010-06-01'
layout: post
tags:
- php
---

Vous l'avez peut être remarqué à vos depends, mais la boite Mail d’Orange filtre les Spams sur le return-path (entre autre) des headers de chaque E-Mail et le problème, c’est que par défaut ce header est à “www-data” lorsque les Mails sont envoyés à partir de la fonction Mail() de PHP. Du coup, vos Mails n'arrivent même pas dans la boite Spams, ils sont tout simplement ignorés.

Prestashop utilise quant à lui une librairie (Swift), pour gérer l'envoie des Mails, et il n’a pas été facile de m’y retrouver afin de fixer ce problème de header, et donc de pouvoir envoyer des Mails aux destinataires Orange. A ma grande surprise, ce sujet -pourtant crucial- n'est que peu abordé dans les différents forums, alors je vous donne une soluce un peu “brutale”, mais qui a le mérite de fonctionner rapidement et sans beaucoup de code.

Une fois dans le répertoire de votre boutique, éditez /tools/swift/Swift/Plugin/MailSend.php, et rendez vous autour des ligne 158 à 161 qui doivent ressembler à ça :$headers = $headers->build();
if (!ini_get("safe_mode")) $success = mail($to, $subject, $message, $headers, $params);
else $success = mail($to, $subject, $message, $headers);
Tout est dans le cinquième argument de la fonction Mail, où pour l’instant $params n’est pas initialisé. On va donc le faire directement ici :

$headers = $headers->build();
$params = "-f" . "administrateur@mon_nom_de_domaine.com";
if (!ini_get("safe_mode")) $success = mail($to, $subject, $message, $headers, $params);
else $success = mail($to, $subject, $message, $headers);
Voila, c’est tout. Je vous conseil aussi d’ajouter un SPF dans votre config de bind, si vous y avez accès, ainsi que valider votre domaine auprès du “sender-ID program” de chez Microsoft, si en prime vous voulez que les destinataires de chez Hotmail reçoivent eux aussi vos messages.

Pfiouuu…contourner les Anti spam maison des uns et des autres, franchement, c’est l’enfer.
