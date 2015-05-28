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
  $git config --global color.ui auto
  
  Commande Git
    - Voir dans quel état on se trouve ? 
      -> $git status
    - Modifier / ajouter des fichiers 
      -> $ git status
      -> les fichiers modifiés
      -> les fichiers non suivis par git (ajoutés)
    - Voir les différences 
      -> $git diff
    - Enregistrer les modifications (faire un commit)
      -> Ajouter les changements à enregistrer dans l'index: $git add fichier1 fichier2 ...
      
     $git status (pour vérifier)
        $git diff
        $git diff --cachcd
      
      -> Faire le commit (enregistrer les changements): $git commit
      
     $git status
    
    - Raccourcis
      -> $git commit -& : fait automatiquement le "add" pour les fichiers déjà connus de git
      -> $git commit -- fichier: le fichier est ajouté pour le commit
      -> $git commit -m "Message ..."
      
    - Revoir les commits
      -> $gitk : affiche le dépôt avec la liste des commits
      -> $git log : même affichage que précédement 
      -> $git log -p : affichage des fichiers modifiés
      -> $git log --stat --summary : information sur les fichiers modifiés et quantité de choses modifiées sur chaque fichier       -> $git log --oneline : chaque commit est résumé sur une seule ligne
      
    - Envoyer / recevoir les modifications vers / depuis un serveur 
      -> envoyer: $git push : récupère et intègre les changements
      -> recevoir: $git pull
                   $git fetch : récupère les changements 
    - A quoi peuvent ressembler des "vrais" commits
      -> en général: changements unitaires
                     message explicatif
    Exemple: https://git.kernel.org  -> choisir git.git -> log 
    
    - Ajout, suppression des fichiers
      -> Ajout: git add fichiers ....
      -> Supression: git rm fichiers ....
      -> Renommer / Déplacer: git mv fichiers .... 
      
      Remarque: en pratique, ça revient à une suppression et un ajout. on peut le constater avec: git log --summary 
                                                                                                  git log --summar -M
    
    - Mettre du travail de côté : 
      * git stach: met les modifications de côté (pile)
      * git stash pop : dépile et applique les dernières modifications sauvegardées par git stash
      * git stash drop
      * git stash show
      * git stash list
    
    - Fichier ".gitignore
      -> pour éviter d'enregistrer des données personnelles ou a risque d'être pirater, créer un fichier ".gitignore" où ser listé toute une liste des fichiers à ne pas enregistrer comme: 
        * "~"
        * ".back"
        * ".o"
        * ".class"
        * essai.java"
        
    Remarque: à enregistrer dans le dépôt
    
      -> man gitignore
    
    - Les branches
      -> création: git branch experimental
      -> lister les branches: git branch (avec à côté une "*" qui se mettra en face de la branche sur laquelle on se trouve)
      -> changer de branche: git checkout experimental
      
      Ex: aditer des fichiers, enregistré (commit) -> git checkout mmaster
          faire d'autres modificatins (+ commit)
          git merge experimental : cela prend une branche à laquelle il intègre ls changements
          
      Si conflit, le merge s'arrête et les points problématiques sont indiqués. pour les voir : git diff
      Ensuite: git commit -a
      
        -> supprimer une branche: git branch -d experimental
       Remarque: ne fonctionne que si celle-ci à été intégrée à une autre branche sinon la commande ne s'effectuera pas. car on perd tout. 
       
       -> Pour forcer la suppression: gir branch -D (branche foireuse)
    
    - Etiqueter une version
    
      -> git tag nom [commit] // entre crochets, cela permet de préciser quel commit l'on souhaite utiliser
  exemple: git tag v1.0
  
      -> pour lister les tags existant: git tag
// pour les différentes manières d'identifier un commit -> man gitrevisions

  - Identifier l'origine des changements 
    -> git blame fichier

  - Identifier le commit à l'origine d'un problème
    -> git bisect // permet de dire telle version était bonne et celle-ci ne l'était pas. ensuite il sort une version qui se trouve entre les deux et vous demande si c'est bon ou non. cela jusqu'à ce qu'il trouve la version qui correspond. 

  exemple: $ git bisect start // permet de commencer la recherche
           $ git bisect bad // permet de dire que la version actuelle n'est pas bonne
           $ git bisect good v1.52 // permet de dire que telle version est bonne
           $ git bisect good ou bad 
    
    - Pour faire des commits propres (courts, unitaires, etc.)
      => séléctionner ce qu'on ajoute pour un commit
        -> git add -p [fichier]
    
    - Annuler un commit
      -> git revert identifiant
      
    - Compléter le dernier commit 
      -> ATTENTION: avant de partager avec git push par exemple
      
      -> git commit --amend
    
    - Annuler des changements / les derniers commits
      -> ATTENTION: A éviter si les commits ont déjà été partagés
      -> git reset [mode] [identifiant de commit]
      -> ATTENTION: par défaut l'identifiant de commit est HEAD
        > réinitialise le dépôt sur le commit donné
        > mode : --soft -> réinitialise le dépôt seulement
                 --mixed -> réinitialise le dépôt et l'index (mode par défaut)
                 --hard -> réinitialise tout (répertoire de transit compris)
                 
        > par exemple: $ git reset HEAD^^ -> supprime les deux de'rniers commits
        > par exemple: $ git reset --hard -> réinitialise le répertoire de travail sur le dernier commit et supprime toutes les modifications
    
    - Avant de faire un push, on aimerait revenir sur les derniers commits (pour les compléter, en supprime, en changer l'ordre, etc.).
        > version sur le serveur sera: origin/master 
      -> git rebase -i origin/master
        > -i : mode interactif -> un éditeur est lancer avec la liste des commits qui vont être appliqués
          - pick 73a42f blablabla
          - pick 7217cd UnAutreCOmmit
          
      -> si on remplace pick par switch up ou fixe up, alors les commits seront fusionnés 
        
        > si problème, le rebase s'arrête pour qu'on puisse le corriger (conflit par exemple) 
        > ensuite on fait : git rebase --continue
        > on peut aussi faire: git rebase --skip (pour ignorer le commit qui pose problème)
        > ou ausssi: git rebase --adopt (pour annuler l'opération rebase) 
        
        > git pull --rebase
      
    - Créer un départ git local
      -> git init (Dans un répertoire donné)
      
    - Récupérer (fiare une copie) un dépôt
      -> git clone /chemin/vers/dépôt/
      -> git clone ss://login@machine/chemin/vers/depot/
      -> git pull pour récupérer les dernières modifications
      
    - Travailler à plusieurs
      > man gittutorial "using git for collaboration"
