# Test
Première séance TP

Vue Principale 
  - liste des fichiers
  - contenu du fichier README

Pour un fichier donné (en cliquant sur son nom)
  - Résumé de la dernière modification du fichier (commit)
  - contenu du fichier
    * en cliquant sur "initial commit"
      * détails du commit
      * message associé
      * auteur et date
      * identifiant de commit (somme SAH-1), suite de 40 chiffres en hexadécimal
      * détails des modifications

Possibilité de modifier le fichier en ligne grâce au petit crayon

Pour récupérer une copie en local, ouvrir la commande et: 
- $ git clone https://github.com/login/Test.git
- en SSH: git@github.com:login/Test.git

NB: posiionner la variable d'environnement: export https_proxy=proxy.iut_bm.univ-fcomte:3128

En local: 
  Test/README.md
    - .git/-config

Visibilité graphique: 
  - git k (dans la console, se mettre dans le dossier concerné et ensuite tapé gitk --all)

Efficacité de git : 
- exemple du noyau Linux: version actuelle fait 49 000 ficchiers dans 3158 répertoires et environ 648 M
- exemple de git: depuis 2005 -> 500 000 commits, 999 M

Outil en ligne de commande : git
- usage: ~$ git commande[parametre ...]
- aide: ~$ man ou git help
  * ex: $man git-clone
        $git help clone

Un peu de paramétrage: 
  $git config --global user.name "Prenom Nom"
  $git config --global user.email "adresse@email"

