---
title: Initialiser un repo Git pour les nuls
date: '2011-02-06'
layout: post
tags:
- la-technique
---

Admettons que vous soyez dans la situtation suivante :*Vous disposez d'un serveur dédié sur lequel vous hébergez (ou voulez héberger) une working copy (votre appli en prod, par exemple) et votre repository SVN


*Vous voulez quitter SVN pour GIT, mais n'êtes pas encore un expert en la matière


*Vous n'avez que faire de l'historique de vos commit, de vos branches... vous voulez juste repartir de 0 avec Git (sinon, voyez plutôt
[Git-SVN](http://www.kernel.org/pub/software/scm/git/docs/git-svn.html))


*Vous souhaitez simplement créer un dépot Git et démarrer du bon pied rapidement
Vous êtes aussi dans ce même cas de figure ?! Dans cet exemple, j'utilise deux machines : @server via SSH et @local qui est mon PC, au chaud chez moi.

 

# Côté serveur, on commence par se créer un répertoire qui hébergera le serveur "bare" (=le dépot SVN)

guillaume@server:$ mkdir /var/local/git/repos/my_app
# On initialise ce repo

guillaume@server:$ cd /var/local/git/repos/my_app && git --bare init
Initialized empty Git repository in /var/local/git/repos/my_app/
# Nous voila maintenant avec un repo GIT "bare", un peu comme un repo SVN. Si on regarde à l'intérieur, ça donne ça :

$ ls
branches config description HEAD hooks info objects refs
# On revient chez soi, en local, et on supprime récursivement tous les .svn du projet

guillaume@local:$ cd /home/guillaume/my_app/
guillaume@local:$ rm -rf `find . -type d -name .svn`
# Puis on initialise le projet, cela va créer un répertoire .git à la racine, contenant -entre autre- les fichiers de conf

guillaume@local:$ git init
Initialized empty Git repository in /home/guillaume/my_app/.git/
# On informe maintenant la copie locale de l'existence du repo sur notre serveur (évidemment, remplacez 81.81.81.81 par l'adresse de votre serveur). Par convention on appellera ce repo "origin"

guillaume@local:$ git remote add origin ssh://81.81.81.81/var/local/git/repos/my_app
# On informe Git des fichiers qu'il faut tracker. Dans notre cas, on ajoute tout le répertoire, soit simplement "."

guillaume@local:$ git add .
# Ok, on peut faire notre premier commit :

guillaume@local:$ git commit -a -m 'initialize repo'
[master (root-commit) 7871087] initialize repo
23 files changed, 500 insertions(+), 0 deletions(-)
create mode 100755 build.properties
create mode 100755 build.xml
.....
# On a presque terminé : il faut maintenant tout monter sur notre repo "origin", dans la branche "master" :

guillaume@local:$ git push origin master
Counting objects: 44, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (31/31), done.
Writing objects: 100% (44/44), 1.65 MiB, done.
Total 44 (delta 1), reused 0 (delta 0)
To ssh://81.81.81.81/var/local/git/repos/my_app
* [new branch] master -> master
# Et voila ! Si on retourne sur notre serveur, on a plus qu'à "cloner" (= checkout sur SVN) notre appli :

guillaume@server:$ git clone file:///var/local/git/repos/my_app
# On peut vérifier que tout marche en faisant quelques modifs dans des fichiers en local, puis :

guillaume@local:$ git commit -a -m "Add some killer features"
[master 51401e0] add
 1 files changed, 2 insertions(+), 0 deletions(-)
 mode change 100644 => 100755 app/views/demo.html.haml

guillaume@local:$ git push
Counting objects: 13, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (7/7), done.
Writing objects: 100% (7/7), 595 bytes, done.
Total 7 (delta 5), reused 0 (delta 0)
To ssh://81.81.81.81/var/local/git/repos/my_app
   ef4d530..51401e0  master -> master
# On revient sur le serveur, et on "pull"

guillaume@server:$git pull
remote: Counting objects: 13, done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 7 (delta 5), reused 0 (delta 0)
Unpacking objects: 100% (7/7), done.
From file:///var/local/git/repos/my_app
   ef4d530..51401e0  master     -> origin/master
Updating ef4d530..51401e0
Fast forward
 controllers/application_controller.rb     |    2 ++
 1 files changed, 2 insertions(+), 0 deletions(-)
 mode change 100644 => 100755 app/views/demo.html.haml
Ce tuto est librement inspiré de
[celui-ci](http://crashingdaily.wordpress.com/2009/09/02/initing-a-new-remote-git-repository-with-existing-files/) en Anglais, qui m'a beaucoup aidé à faire mes premiers pas.
