# Git 

## Configurer Git 

**Changer editeur de texte pour vscode par exemple** : ```git config --global core.editor "code --wait"``` 

**Configuration nom utilisateur et email**
```git config --global --edit```

## Commandes de bases

- ```git init```
- ```git add``` + nom des fichiers (sépararés par espace) ou "." pour tout ajouter. Ajoute les fichiers à commit dans une "zone de transit" avant de les commit
- ```git status``` affiche les fichiers non trackés, ceux modifiés, etc...
- ```git commit -m "le message que l'on souhaite ajouter"``` créer la sauvegarde 
- ```git commit -a -m "le message"``` Fera automatiquement un add des fichiers modifiés (pas ceux ajoutés)
- ```git log``` affiche la liste des commits effectués (HEAD) étant le plus récent

**Git amend**
Si lors d'un commit on a oublié quelque chose, par exemple le fichier script.js

```git add script.js```
```git commit --amend``` Ouvrira l'editeur de texte, permettant de modifier le message du dernier commit, et les fichiers ajoutés


## Branch & Merge

- ```git branch``` la branch sur laquelle on se trouve, de base 'master'
- ```git branch newbranch``` créer une nouvelle branche s'appelant newbranch, qui sera une copie de master
- ```git switch newbranch``` on switch à la branch newbranch
- ```git switch -c newbranch``` crée la branch newbranch, et switch dessus en meme temps


#### Sans Conflit
Si des changements ont été fait sur la newbranch, mais pas sur la master, on peut merge les deux branches sans conflit:
- ```git switch master``` on retourne sur master
- ```git merge newbranch``` on fusionne newbranch avec master. 

#### Avec Conflit
Si des changements ont été fait sur newbranch et sur master, sur le meme fichier par exemple, il peut y avoir des conflits. 
- ```git merge newbranch``` console output : CONFLICT (content): Merge conflict in 'thisfile'

Les conflits apparaitront alors sur vscode, et on pourra manuellement choisir ce que l'on veut garder.
Une fois fait, refaire un ```git add thisfile``` et enfin ```git commit -m "conflit résolu"```


#### Merge par recursion

Si des changements ont lieu sur les deux branches, mais qu'aucun ne font de conflit avec l'autre, il est possible de merge. Même si des changements ont lieu sur le même fichier, tant qu'ils sont sur des lignes différentes.


### Supprimer et renommer

On ne peut pas supprimer de branch si l'on se trouve dessus.

```git branch -d nomDeLaBranche``` 
```git branch -D nomDeLaBranche``` si des changements non commit ont été faits sur la branch et que l'on veut tout de même la supprimer 

Pour renommer une branch, il faut se placer dessus.

```git branch -m newName```

### Visualiser les différences

```git diff```  tous les changements depuis le dernier commit s'affichent dans la console

"-" ce qui a été retiré
"+" ce qui a été ajouté


## Checkout

git checkout permet de faire plusieurs choses.

- ```git checkout main``` : sort de l'actuellement et va sur la main. Même chose que git switch
 
- ```git log``` pour avoir les id des commits précédents
- ```git checkout b3f294f19d18d8182520f59eb11b1fe595004128``` : on peut "voyager" dans nos anciens commits

Il peut être difficile de s'y retrouver dans l'historique des commits. Pour cela on peut rajouter des tags à nos commits.
Exemple : on veut pouvoir retrouver facilement le commit b3f294f19d18d8182520f59eb11b1fe595004128 :
- ```git checkout b3f294f19d18d8182520f59eb11b1fe595004128``` on se déplace sur le commit que l'on veut tag
- ```git tag nomdutag``` /// ```git tag``` pour lister les tag
- Maintenant si l'on veut y retourner facilement : ```git checkout nomdutag```

Pour supprimer un tag: 
- ````git tag -d nomdutag```

**Si beaucoup de commit dans le log**
- ```git log --oneline``` : affiche les commits sur une ligne, pour plus de lisibilité. Les petits id sont utilisables pour checkout dessus. 

## Git restore

Pour retourner à l'état du dernier commit: ```git restore```

Si l'on a add un fichier que l'on ne veut finalement pas commit:
- ```git restore --staged nomDuFichier```

## Reset & Revert

Si par exemple on vient de faire un commit contenant certaines modifications qui ne nous plaisent pas, et que l'on veut retourner à celui d'avant:

- ```git reset idducommitouonveutretourner``` : On retournera à ce commit, mais les modifications effectuées ne disparaitront pas. 
- ```git reset --hard idducommit``` : on retournera à ce commit, et toutes les modifs seront supprimées

Si l'on vient de faire un commit, que l'on souhaite garder, mais ne pas mettre en place tout de suite

- ```git revert idducommitquelonveutgarder``` : on va "sauter" ce commit et continuer de travailler sur l'avant-dernier commit

## Cherry-Picking

Exemple avec deux branches, main et second
Deux commits fait sur second: commit1 et commit2
On ne veut ajouter que le commit1 à la branch main
- git log
- on récupère l'id du commit1
- On switch sur main
- ```git cherry-pick idcommit1```


# GitHub

Pour cloner un repot distant, avec tout l'environement git qui va avec

```git clone adressedurepot``` Créera un dossier avec le nom du repot. 

```git remote -v``` affiche le nom du repot distant, et l'url 

Cliquer sur fork sur Github pour copier un repot sur son profil.

### Push & pull 


```git push -u origin main``` Crée la branch main sur le repot distant et envoie le/les commits.

Pour les prochains push juste besoin de faire : ```git push```

Si on est sur une branch 'second' nouvellement créée :```git push -u origin second```

Si on veut demander à merge notre branch second à la main, on peut faire une pull request sur Github.
Le responsable de la main pourra alors accepter ou pas de le faire, en fonction des conflits où d'éventuelles erreurs. 


