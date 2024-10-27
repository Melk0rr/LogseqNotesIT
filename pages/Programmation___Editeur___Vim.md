# Introduction
collapsed:: true
	- Editeur de texte #OpenSource publié en 1991 qui repose sur un système de modes et de raccourcis permettant une manipulation et une navigation rapide et efficace d'un document
- # Commandes
	- ## Mode normal
		- ### Navigation de base
		  collapsed:: true
			- Vers la **gauche** : `h`
			- Vers le **bas** : `j`
			- Vers le **haut** : `k`
			- Vers la **droite** : `l`
			- De **10 lignes vers le bas** : `10j`
			- De **10 caractères vers la droite** (etc.): `10l`
		- ### Navigation dans le document
		  collapsed:: true
			- Vers le **haut du document** : `gg`
			- Vers la **fin du document** : `G`
			- D'une **demie page vers le bas** : `Ctrl+d`
			- D'une **demie page vers le haut** : `Ctrl+u`
			- Vers la **ligne numéro 50** (fonctionne avec n'importe quel numéro de ligne) : `50G`
			- De **10 lignes vers le haut** : `10k`
		- ### Navigation dans la ligne
		  collapsed:: true
			- Vers la **fin de la ligne** : `$`
			- Vers le **début de la ligne** : `0`
			- Vers le **début de la ligne** (au **premier caractère non vide**) : `^`
			- Au **premier caractère** du **mot suivant** (*word*) : `w`
			- Au **premier caractère** su **mot précédent** (*backward*) : `b`
			- Au **premier caractère** du **mot suivant** en **ignorant les caractères spéciaux** : `W`
			- Au **premier caractère** du **mot précédent** en **ignorant les caractères spéciaux** : `B`
			- Au **dernier caractère** du **mot suivant** (*end*): `e`
			- Au **dernier caractère** su **mot précédent** : `ge`
			- Jusqu'à la **prochaine occurrence d'un caractère** (ici: "**z**") (*find*): `fz`
			- A l'occurrence **précédente** / **suivante** du **caractère précédemment recherché** (**f**) : `,				  ```
		- ### Navigation dans le paragraphe / block
		  collapsed:: true
			- Au **paragraphe précédent** : `{`
			- Au **paragraphe suivant** : `}`
			- Vers la **paire** de **parenthèse** / **crochet** / **accolade** : `%`
		- ### Manipulation de document
		  collapsed:: true
			- **Undo** / **défaire** (équivalent au *Ctrl+Z*) (*undo*) : `u`
			- **Redo** / **refaire** (équivalent au *Ctrl+Y*) (*redo*) : `Ctrl+r`
			- **Change** et passe en mode **insertion** pour remplacer **mot** / **ligne**
			  collapsed:: true
			  ```vim
			  cw
			  cc
			  c$
			  c0
			  c^
			  cG
			  cgg
			  ```
			- Supprimer **mot** / **ligne** / etc suivant (*delete*)
			  ```vim
			  dw
			  diw
			  d2w
			  d10w
			  dd
			  d$
			  d0
			  d^
			  dG
			  dgg
			  ```
			- **Supprimer** tout le contenu compris entre les **parenthèses** / **crochets** / **accolades** / **guillemets** 
			  ```vim
			  di(
			  di[
			  di{
			  di"
			  di'
			  ```
			- Supprimer **tout le document** :`ggdG`
			- Copier **caractère** / **mot** / **ligne** / etc (*yank*)
			  ```vim
			  yl
			  y4l
			  yh
			  y6h
			  yw
			  yiw
			  y5w
			  yy
			  y$
			  y0
			  y^
			  yG
			  ygg
			  ```
			- Copier **tout le document** : `ggyG`
			- Coller sur la **ligne suivante** (*paste*) : `p`
			- Coller sur la **ligne précédente** : `P`
				- ### Changement de mode
				  collapsed:: true
				- Revenir au mode **normal** 
				  ```vim
				  Esc
				  ```
				- #### Insertion
				  collapsed:: true
				- Passer en mode **insertion** à l'emplacement du curseur 
				  ```vim
				  i
				  ```
				- Passer en mode **insertion** à la **fin de la ligne**
				  ```vim
				  A
				  ```
				- Passer en mode **insertion** à la **ligne suivante** 
				  ```vim
				  o
				  ```
				- Passer en mode **insertion** à la **ligne précédente** 
				  ```vim
				  O
				  ```
				- #### Visual
				  collapsed:: true
				- Passer en mode **visual line** 
				  ```vim
				  V
				  ```
				- Passer en mode **visual block** 
				  ```vim
				  Ctrl+v
				  ```
				- ## Mode édition / insertion
				  collapsed:: true
				- Mode d'édition de texte
				- ## Mode visual
				  collapsed:: true
				- Mode de **sélection** de texte
				- Comprend 2 sous-modes : **line** et **block**
				- ### Ligne
				- ### Block
				- ## Mode command-line
				  collapsed:: true
				- ### Manipulation de document
				  collapsed:: true
				- **Quitter** le document 
				  ```vim
				  :q
				  ```
				- **Sauvegarder** les changements 
				  ```vim
				  :w
				  ```
				- **Sauvegarder** et **quitter** le document 
				  ```vim
				  :wq
				  ```
				- **Forcer** la **fermeture** du document sans sauvegarder 
				  ```vim
				  :q!
				  ```
				- **Copier tout le document** 
				  ```vim
				  :%y
				  ```
				- **Supprimer tout le document** 
				  ```vim
				  :%d
				  ```
				- **Remplacer** toutes les **occurrences d'une chaîne** 
				  ```vim
				  :%s/foo/bar/g
				  ```
				- ### Recherche
				  collapsed:: true
				- **Rechercher** une **chaîne** 
				  ```vim
				  /chaîne à rechercher
				  ```
				- **Rechercher** une chaîne en **partant de la fin** 
				  ```vim
				  ?chaîne à rechercher
				  ```
				- **Sélectionner** le **premier élément trouvé** 
				  ```vim
				  ENTER
				  ```
				- Aller à l'élément trouvé **suivant** 
				  ```vim
				  n
				  ```