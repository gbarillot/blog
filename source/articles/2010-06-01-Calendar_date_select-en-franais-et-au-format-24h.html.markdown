---
title: Calendar_date_select en français et au format 24h
date: '2010-06-01'
layout: post
tags:
- la-technique
- ruby-on-rails
---

Obtenir des dates correctement formatées dans une interface “user-friendly” est très souvent utile au sein d’une application. Pour arriver à vos fins facilement, rapidement et efficacement, il existe de nombreux Plugins pour Rails. Après en avoir testé plusieurs, j’ai fini par m’arrêter sur
[Calendar Date Select](http://code.google.com/p/calendardateselect/) . Un bon plugin, bien fichu, basé sur la librairie Prototype. Le seul “petit” problème, c’est que la documentation est assez foutraque, les formats de date par défaut sont au format américain “mois/jour/année” et les heures en deux cadrans (5 PM et 5 AM). J’ai donc du me battre avec la doc et creuser dans le code pour arriver à mes fins. Tant qu’à faire, autant partager mes résultats, si ça peut profiter à d’autres…


**Note**
 :
Ceci n’est probablement pas la solution la plus élégante ni la plus “propre”, mais cela à le mérite de fonctionner parfaitement, et d’être déployable rapidement.


**# Installation :**


Il est possible d’installer calendar date select via un Gem, mais je préfère le Plugin, afin d’accéder sans souci aux différents fichiers :git clone git://github.com/timcharper/calendar_date_select.git vendor/plugins/calendar_date_select && rm -rf vendor/plugins/calendar_date_select/.git
Il faut ensuite inclure les fichiers JS dans votre header. Rajoutez la ligne suivante dans votre layout :

<%= calendar_date_select_includes "default" %>
Le “default” représente la skin utilisé, vous pouvez aussi choisir parmi les skins présentes dans votre répertoire “/public/stylesheets/calendar_date_select”

Ajoutez maintenant la ligne suivante dans votre template, en lieu et place de l’emplacement de votre champ date

<%= calendar_date_select_tag "le_nom_de_mon_champ_date", "", :time => true, :style=>'width:220px;' %>
… et hop, vous devriez pouvoir afficher le calendrier au clic sur l’icone à droite du champ. Il ne nous reste “plus qu’à” afficher une date en Français et au format 24h

 


**#configuration des jours et des mois :**


Nous allons nous baser sur le format “Euro_24h”, le plus proche de celui qu’il nous faut. Ajoutez la ligne suivante dans votre “environmement.rb”

CalendarDateSelect.format = :euro_24hr
Avec ça, le helper que vous avez placé plus haut dans votre header va automatiquement inclure le fichier “/public/javascripts/calendar_date_select/format_euro_24h.js”

Ok, il s’agit maintenant de renseigner les noms des mois et des jours. Editez le fichier “/javascript/calendar_date_select/format_euro_24h” et ajoutez les tableaux suivants :

Date.full_weekdays = $w("Dimanche Lundi Mardi Mercredi Jeudi Vendredi Samedi");
Date.weekdays = $w("Di Lu Ma Me Je Ve Sa");
Date.months = $w("Janvier Fevrier Mars Avril Mai Juin Juillet Aout Septembre Octobre Novembre Decembre" );
… on ajoute aussi le nom du jour dans le champ date. Remplacez la première ligne de la fonction par celle ci :

str = Date.full_weekdays[this.getDay()] + " " + Date.padded2(this.getDate()) + " " + Date.months[this.getMonth()] + " " + this.getFullYear();
Votre fichier “/javascript/calendar_date_select/format_euro_24h” ressemble donc à ça :

Date.prototype.toFormattedString = function(include_time)
{
  //alert(this.getDay());
   str = Date.full_weekdays[this.getDay()] + " " + Date.padded2(this.getDate()) + " " + Date.months[this.getMonth()] + " " + this.getFullYear();
   if (include_time) { str += " " + this.getHours() + ":" + this.getPaddedMinutes() }
   return str;
}

Date.full_weekdays = $w("Dimanche Lundi Mardi Mercredi Jeudi Vendredi Samedi");
Date.weekdays = $w("Di Lu Ma Me Je Ve Sa");
Date.months = $w("Janvier Fevrier Mars Avril Mai Juin Juillet Aout Septembre Octobre Novembre Decembre" );
Si vous testez comme tel, vous devriez obtenir un calendrier avec des jours de de type “Lu, Ma, Me…”, et qui vous retourne une date du type “Mardi 1 juin 2010 11:20. C’est déja bien, mais le champ de selection de l’heure est -lui- toujours au format anglo-saxon “AM/PM”. (note : c’est là que ce tuto dérape un peu et est à mon avis un peu “intrusif”, mais bon… si quelqu’un a une solution plus élégante, je suis preneur). Ouvrez maintenant le fichier “/public/javascript/calendar_date_select/calendar_date_select.js”, et éditez les deux méthodes suivante, autour de la ligne 30 :

Date.prototype.getAMPMHour = function() { var hour = this.getHours(); return (hour == 0) ? 12 : (hour > 12 ? hour - 12 : hour ) }
Date.prototype.getAMPM = function() { return (this.getHours() < 12) ? "AM" : "PM"; }
… modifiez les afin d’obtenir ça :

Date.prototype.getAMPMHour = function() { var hour = this.getHours(); return (hour == 0) ? 0 : (hour > 24 ? hour - 24 : hour ) }
Date.prototype.getAMPM = function() { return (this.getHours() < 12) ? "" : ""; }
… et voila !
