---
title: Cinq bonnes raisons d'aimer Ruby
date: '2011-01-27'
layout: post
tags:
- la-technique
- ruby-on-rails
---

Cela faisait très longtemps que j'avais ce post en tête, j'avais vraiment envie de mettre à plat quelques unes des raisons
qui font qu'il m'est maintenant pénible de revenir à PHP (non, c'est pas un troll, j'explique, c'est tout !).
Voici donc 5 aspects particulièrement pratiques à mes yeux en ce qui concerne mon utilisation quotidienne de Ruby :***Tout est objet **
Oui, je sais, on vous a déja fait le coup avec Java, mais là c'est vrai. Même avec les types primitifs. Le
nombre "1" par exemple, est un objet comme les autres.
**Exemple :**


5.times{puts "hello"}
hello
hello
hello
hello
hello
Et pour connaitre toutes les méthodes d'un objet, c'est aussi très simple : "1.methods" dans le cas présent vous dira tout ce qu'il est possible de faire avec votre nombre "1".
Tout ça peut paraitre un peu gadget présenté comme ça, mais le GROS avantage que j'y vois par rapport aux autres languages, c'est qu'on a plus de question à se poser : tout, absolument tout, est objet. Pas d'exception à rajouter dans mon petit cerveau encombré, c'est déja ça de gagné.


***La syntaxe **
Avec "la syntaxe", je suis vraiment large et regroupe volontairement un paquet de choses, mais ce seul "la syntaxe" est un argument de poids quand vous passez 10 heures/jour devant votre écran.
Je ne sais pas vous, mais moi en tout cas, le camelCase les () ; et autres {} ça me fait mal aux yeux.

**Exemple**


# Ruby
if my_flag == true
  Stuff.do_this_little_trick_with "a string"
else
  Stuff.do_not_do_it
end
Avouez quand même que par rapport à ça

# PHP
if(my_flag == true){
  Stuff->doThisLittleTrickWith("a string");
}
else {
  Stuff->doNotDoIt();
}
C'est quand même plus lisible, non ? Cet exemple est archi simple, mais quand vous avez plusieurs centaines de lignes dans une classe codée il y a un plus d'un an, (ou codée par quelqu'un d'autre) croyez moi, on apprécie...


***Les attributes accessors**
Il y a plusieurs façon de renvoyer plusieurs attributs en sortie d'une classe. La plus évidente est sous forme de tableau. D'ailleurs, bien souvent, vous n'avez pas trop le choix, à moins de créer une méthode uniquement pour pouvoir accéder à vos attributs avec une notation objet plus pratique et élégante. En ce qui me concerne, moins j'en fais et mieux je me porte, d'autant que Ruby met à ma disposition les attr_accessors. Hy-per-pra-tique

**Exemple :**


class User

  attr_accessor :phone, :first_name, :last_name

  def initialize(phone, first_name, last_name)
    @phone = phone
    @first_name = first_name
    @last_name = last_name
  end

end

=> new_user = User.new("0812 01 02 03", "Guillaume", "Barillot")
=> new_user.first_name # => "Guillaume"
Ca n'a l'air de rien, mais l'essayer, c'est l'adopter !


***La console**

Mon premier language était Python (où la console existe aussi depuis toujours), ceci explique peut être cela, mais j'ai toujours apprécié d'avoir une console sous la main. Vous ne vous rappelez plus de la syntaxe de tel appel ? Vous avez un doute sur ce que
va faire votre boucle ? Hop, un petit tour en console et vous êtes fixé, pas besoin de relancer tout votre process et votre page Web.

**Exemple :**


irb > 5.Time.puts "hello"
NoMethodError: undefined method `Time' for 5:Fixnum
	from (irb):19
	from :0
# Ha bon ?

irb > 5.times{puts "hello"}
hello
hello
hello
hello
hello
# Vooooila, c'est ça, j'avais juste oublié les brackets


***La gestion des dates et du temps**
Alors ça, la première fois que je m'en suis servi, j'ai vraiment eu du mal à y croire ! Quiconque s'est déja essayé à coder un calendrier ou -pire- un outil de gestion de planning s'est forcément cassé les dents là dessus. Avec Ruby, économisez sur votre budget dentiste, tout est simple et intégré d'origine, sans avoir recours à une librairie supplémentaire.

**Exemple :**


# Vous avez besoin des jours compris entre le 27 Février 2011 et le 2 Mars 2011
(Date.new(2011, 2, 27)..Date.new(2011, 3, 2)).each { |x| puts x.day }
# => 27 28 1 2
# Même chose en 2012 ?
(Date.new(2012, 2, 27)..Date.new(2012, 3, 2)).each { |x| puts x.day }
# => 27 28 29 1 2
# Hoooo, une année bisextile !
Voila, j'éspère vous avoir donné envie de vous plonger dans cet excellent language qu'est Ruby.

Petite anecdote : devoir quitter PHP pour Ruby était l'un des freins majeur qui me faisait résister au Framework "Ruby on Rails". Finalement, et très honnêtement, je n'ai jamais eu l'impression "d'apprendre" quelque chose, dans le sens "on commence de rien et on suit péniblement la courbe d'apprentissage". En fait, si vous connaissez la Programmation Orientée Objet, que vous êtes déja à l'aise dans un autre language, et si en plus vous avez déja exploré un peu Python, je le dis sans exagérer : il n'y a pas de courbe d'apprentissage ! Vous pouvez réellement prendre en main ce language en quelques heures seulement.

Vous utilisez déja Ruby et j'ai oublié de parler d'un aspect qui vous plait particulièrement ? Laissez votre commentaire !
