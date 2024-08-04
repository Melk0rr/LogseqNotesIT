# Introduction
	- Editeur de texte #OpenSource publié en 1991 qui repose sur un système de modes et de raccourcis permettant une manipulation et une navigation rapide et efficace d'un document
- # Commandes
	- ## Mode normal
	  collapsed:: true
		- ### Navigation
		  collapsed:: true
			- #### Base
			  collapsed:: true
				- Déplacement vers la **gauche** 
				  ```vim
				  h
				  ```
				- Déplacement vers le **bas** 
				  ```vim
				  j
				  ```
				- Déplacement vers le **haut** 
				  ```vim
				  k
				  ```
				- Déplacement vers la **droite** 
				  ```vim
				  l
				  ```
				- Déplacement de **10 lignes vers le bas** 
				  ```vim
				  10j
				  ```
				- Déplacement de **10 caractères vers la droite** (etc.)
				  ```vim
				  10l
				  ```
			- #### Document
			  collapsed:: true
				- Déplacement vers le **haut du document** 
				  ```vim
				  gg
				  ```
				- Déplacement vers la **fin du document** 
				  ```vim
				  G
				  ```
				- Déplacement d'une **demie page vers le bas** 
				  ```vim
				  Ctrl+d
				  ```
				- Déplacement d'une **demie page vers le haut** 
				  ```vim
				  Ctrl+u
				  ```
				- Déplacement vers la **ligne numéro 50** (fonctionne avec n'importe quel numéro de ligne) 
				  ```vim
				  50G
				  ```
				- Déplacement de **10 lignes vers le haut** 
				  ```vim
				  10k
				  ```
			- #### Ligne
			  collapsed:: true
				- Déplacement vers la **fin de la ligne** 
				  ```vim
				  $
				  ```
				- Déplacement vers le **début de la ligne** 
				  ```vim
				  0
				  ```
				- Déplacement vers le **début de la ligne** (au **premier caractère non vide**) 
				  ```vim
				  ^
				  ```
				- Déplacement au **premier caractère** du **mot suivant** (*word*) 
				  ```vim
				  w
				  ```
				- Déplacement au **premier caractère** su **mot précédent** (*backward*) 
				  ```vim
				  b
				  ```
				- Déplacement au **premier caractère** du **mot suivant** en **ignorant les caractères spéciaux** 
				  ```shell
				  W
				  ```
				- Déplacement au **premier caractère** du **mot précédent** en **ignorant les caractères spéciaux** 
				  ```shell
				  B
				  ```
				- Déplacement au **dernier caractère** du **mot suivant** (*end*)
				  ```vim
				  e
				  ```
				- Déplacement au **dernier caractère** su **mot précédent** 
				  ```vim
				  ge
				  ```
				- Déplacement jusqu'à la **prochaine occurrence d'un caractère** (ici: "**z**") (*find*)
				  ```vim
				  fz
				  ```
				- Déplacement à l'occurrence **précédente** / **suivante** du **caractère précédemment recherché** (**f**) 
				  ```vim
				  ,
				  ;
				  ```
			- #### Paragraphe / block
			  collapsed:: true
				- Déplacement au **paragraphe précédent** 
				  ```vim
				  {
				  ```
				- Déplacement au **paragraphe suivant** 
				  ```vim
				  }
				  ```
				- Déplacement vers la **paire** de **parenthèse** / **crochet** / **accolade** correspondant à celle sur **laquelle est placé le curseur** 
				  ```vim
				  %
				  ```
		- ### Manipulation de document
		  collapsed:: true
			- #### Changements
				- **Undo** / **défaire** (équivalent au *Ctrl+Z*) (*undo*)
				  ```vim
				  u
				  ```
				- **Redo** / **refaire** (équivalent au *Ctrl+Y*) (*redo*)
				  ```vim
				  Ctrl+r
				  ```
				- **Change** et passe en mode **insertion** pour remplacer **mot** / **ligne** / etc 
				  ```vim
				  cw
				  cc
				  c$
				  c0
				  c^
				  cG
				  cgg
				  ```
			- #### Suppression
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
				- Supprimer **tout le document** 
				  ```vim
				  ggdG
				  ```
			- #### Copier / Coller
			  collapsed:: true
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
				- Copier **tout le document** 
				  ```vim
				  ggyG
				  ```
				- Coller sur la **ligne suivante** (*paste*)
				  ```vim
				  p
				  ```
				- Coller sur la **ligne précédente** 
				  ```vim
				  P
				  ```
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