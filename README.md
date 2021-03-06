# Estimateur de note de bac 2020

Ce script python permet d'évaluer et d'estimer une note ainsi qu'une mention pour le bac de 2020 qui sera en contrôle continue. 
Pour ça il la superbe api pronote de Litarvan (https://github.com/Litarvan/pronote-api). En prime le scipt offre un 
compte rendu pdf avec différents scénarios et des graphiques sur les notes de l'année.

## Méthode de calcul

La note est estimé d'après les notes des bulletins des deux premiers trimestres publiés sur pronote et des notes ajoutés dans le fichier 
(voir la rubrique *utilisation*) ainsi que leurs coefficients. Les deux bulletins sont d'abord fusionnées en gardant la moyenne
et les coefficients de chaque matière. Chacune de ces moyennes, arrondies au supérieur (d'après le décret le plus récent) 
correspondent à la note de l'épreuve. Le total de points de l'élève est calculé en multipliant
chacune de ces notes par le coefficient de la matière.

Maintenant vient également les notes des options qui comptent comme bonus. Chaque point au dessus de la moyenne est multiplié
par son coefficient (d'après les coefficients officiels du bac) ou par le double de son coefficient 
(en prennant le coeff. pronote qui est la moitié du coeff officiel). Ces points bonus une fois additionnées sont ajoutés
au total des points de l'élève sans que le total des points maximum ne change.\
Si vous avez des remarques à faire n'hésitez pas à [m'en faire part](http://valentin.cassayre.me/contact).

## Avantage du script

* Automatisé au maximum
* Base du réutilisable pour créer d'autres projets utilisant l'api de pronote en Python, par exemple pour récupérer 
des devoirs, faire des moyennes de notes ou alors récupérer l'emplois du temps
* Les données sont classés et tous les bulletins de la terminale sont utilisable dans un tableur (*output/Trimestre n.csv*)
* Sors le détail de toutes les notes utilisé pour calculer la note et les graphs (*output/Relevé notes.csv*)
* Plus classe que de calculer à la main
* Donne un compte rendu en pdf complet avec les notes et les graphiques

## Limites du script

* L'installation peut être longue
* La connection n'est pas forcément sécurisée
* Certains coefficients peuvent être erronés sur pronote (par exemple les langues vivantes peuvent être les deux coeff. 3)
* Il peut y arriver que le script ne se lance pas et affiche une erreur au niveau de l'académie. Cela s'explique par une 
saturation du serveur de pronote (voir message d'erreur de l'api)
* Il faut avoir pronote pour utiliser le script
* Ce n'est qu'une estimation, la note finale sera surement un peu différente, la méthode de calcul est loin d'être parfaite
et n'est qu'une supposition d'après le premier décret sorti. D'autres facteurs comme les appréciations et le livret scolaire 
vont également compter pour ce bac assez spécial.

# Comment l'utiliser ?

D'abord [téléchargez et décompressez le script](https://github.com/V-def/estimation_bac_pronote) et
[téléchargez et décompressez l'api](https://github.com/Litarvan/pronote-api).
Ensuite allez dans le dossier du script puis dans le dossier 'infos'. Il y a **deux fichiers à remplir** :
1. Le fichier *connection_data.txt* doit contenir les 4 informations suivantes :
   1. *Lien_pronote* s'obtient en se connectant à pronote, il sera de la forme
   *00000000.index-education.net/pronote/eleve/...* mais retirez la partie qui se trouve après
   pronote/ pour obtenir un lien de la forme *00000000.index-education.net/pronote/*.
   2. *Académie* est le nom de l'académie, par exemple *ac-strasbourg* ou *ac-lyon*.
   3. *Utilisateur* est l'identifiant de votre ENT.
   4. *Mot_de_passe* est le mot de passe de votre ENT. 
   Pour une protection des données il est conseillé de ne pas le
   remplir dans le fichier le mot de passe, il vous sera demandé par le script.

2. Le fichier *marks_data* sert à ajouter des notes qui ne sont pas présentes sur pronote. Dans la majorité des cas
il s'agit des épreuves anticipées, mais il peut également s'agir d'une matière qui n'est pas noté sur pronote. 
Pour ajouter la note, sautez une ligne dans le fichier texte et écrivez le nom de la matière en majuscules,
puis un séparateur ';' suivit de la note en question, d'un autre séparateur ';', et enfin du coefficient de la matière. 
Si la matière est une option, indiquer la moitié du coefficient, par exemple le TPE de coefficient 2 devient de coefficient 1.

Une fois ces informations rentrées vous pouvez lancer le script et l'api.

## Sous windows

### Lancer l'api

Pour commencer, [installez *nodejs* si vous ne l'avez pas déjà](https://nodejs.org/dist/v12.17.0/node-v12.17.0-x64.msi) 
([site officiel](https://nodejs.org/en/download/)).

Lancer l'invite de commandes en tappant `cmd` dans la barre de recherche windows, et récupérer le chemin d'accès vers l'api
téléchargé précedemment (chemin d'accès = C:\Users\...\pronote-api-master), puis tapper 'cd ' suivi du chemin d'accès :

`cd C:\Users\...\pronote-api-master`

Ensuite tappez\
`npm i`\
`node index.js`

L'api est lancée et la console devrait afficher :\
`Starting...
---> Pronote API HTTP Server working on 127.0.0.1:21727`

### Lancer le script

Récupérer le chemin d'accès vers le dossier du script (C:\...\estimation_bac_pronote-master) et rentrer dans une 
autre fenêtre de la console (cd + le chemin d'accès) :\
`cd C:\...\estimation_bac_pronote-master`

Puis installez les modules python du script :\
`pip install -r requirements.txt`

Et lancez le script en lançant le fichier ***main.py*** ou en rentrant dans la console\
 `main.py`
 
 Après avoir attendu quelques secondes il devrait afficher :
 `Appuyez sur une touche pour continuer... `
 Ca veut dire qu'il a fini, les résultats se trouvent dans le dossier output. Le bilan se trouve dans le fichier *bilan.pdf*.

## Sous linux

### Lancer l'api

Dans le terminal si ce n'est pas déjà fait installez npm et node\
`$ sudo apt-get install nodejs npm`

Une fois que c'est fait vous pouvez vous rendre dans le dossier de l'api que vous avez téléchargé\
`$ cd usr/.../pronote-api-master`

Puis lancez l'api\
`$ npm i`\
`$ node index.js`

Le terminal devrait afficher\
`Starting...
---> Pronote API HTTP Server working on 127.0.0.1:21727`

### Lancer le script

Rendez vous dans le dossier du script téléchargé et remplit précédemment\
`$ cd usr/.../estimation_bac_pronote-master`

Pour installer les librairies installez pip si ce n'est pas fait\
`$ sudo apt install python3-pip`

Puis installez les\
`$ pip3 install -r requirements.txt`

Maintenant vous pouvez lancer le script\
`$ python3 main.py`

## Les graphiques

Le script crée automatiquement un certain nombre de graphiques, ils sont tous rangés dans le dossier *output/graphs*.
Voici des explications plus claires que leur titre et leur mini légende :

1. Le premier graphique est un nuage de point comparant les notes des différentes matières. L’abscisse des points 
colorés représentent la moyenne de chaque matière, leur taille correspond au coefficient donc au poids de la moyenne 
dans la note finale. La couleur de ces points représente l'écart relatif (la différence) à la moyenne de la classe, 
plus la couleur est dans le haut ou dans le vert, plus la note est bonne par rapport à la moyenne de la classe. \
Les triangles bleus représentent les moyennes des trimestres, trimestre 1 ce sont les triangles orientés vers la droite 
et trimestre 2 vers la gauche. Les barres verticales quant à elles représentent les moyennes de classe dans les 
trimestres correspondants (|). Le carré gris représente la moyenne de classe des deux trimestres.
2. Le deuxième graphique est très proche du dernier, c’est une représentation plus simple qui classe les notes par 
rapport à la moyenne de classe au lieu de leur nom. La note de l'élève est tracé par un rond coloré ayant des 
coordonnées relatives à elle-même en abscisse et à la moyenne de la classe en ordonnée. Comme le précédent la couleur 
représente la différence par rapport à la moyenne de classe et la taille leur coefficient.
3. Le troisième graphique est histogramme, il est encore plus simple qu’avant. Les points correspondent aux points du 
bac, ou au produit entre la note d'une matière et son coefficient. \
Les notes sont ordonnées par rapport a leur nom, mais d’autres informations sont présentes. D'abord il y a la moyenne 
des points des élèves de la classe, puis la moyenne de tes points, la moyenne de tes points avec les notes arrondies au 
supérieur et enfin le maximum de points possibles pour cette matière.
4. Ce graphique est un graphique en boite représentant des informations sur chaque donnée comme la moyenne en vert au 
milieu, ou les quartiles qui représentent ou se trouve la majorité des notes. 
5. Le dernier graphique est également très simple à comprendre, c’est un radar qui met en évidences les écarts des notes. 
Le radar est une représentation d'un graphique avec des lignes dans un repère polaire. Il représente les notes de 
l'élève, ainsi que les notes arrondies de l'élèves et sont comparées à la moyenne de classe dans chaque matière.

#### Des problèmes ? Des idées ? [Contactez moi](http://valentin.cassayre.me/contact)
