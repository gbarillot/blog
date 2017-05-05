---
title: La fonction PHP Mail() et l’antispam d’Orange.fr
date: '2009-10-22'
layout: post
tags:
- php
---

Je viens de découvrir à mes dépends que le Mail d’Orange.fr refuse systématiquement les Mails dont le “Return-Path” n’est pas dûment renseigné. Le message n’est même pas passé en Spam, il n’arrive tout simplement… jamais!

La solution pour PHP, est d’utiliser le cinquième argument au moment de l’appel de la fonction mail (je vous passe le formatage du reste du Mail, y’a déja plein d’autres articles là dessus) :$return_path = "-f" . "postmaster@monsite.fr";
mail($to, $sujet, $message, $header, $return_path);
Quant à Rails, il suffit de bien renseigner son /config/environnement.rb

ActionMailer::Base.delivery_method = :sendmail
ActionMailer::Base.sendmail_settings = {
  :location       => '/usr/sbin/sendmail',
  :arguments      => '-i -t -f postmaster@monsite.fr'
}
En espérant que ça puisse aider quelqu’un afin d’économiser une heure de temps précieux comme je viens de le faire…
