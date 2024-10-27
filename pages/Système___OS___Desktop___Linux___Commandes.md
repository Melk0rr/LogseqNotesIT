# #Documentation
collapsed:: true
	- [Documentation en ligne](https://www.geeksforgeeks.org/linux-commands/)
	  id:: 65217c2c-e35f-404b-91ad-66bac8c07a1d
	- [man](https://www.geeksforgeeks.org/man-command-in-linux-with-examples/) <commande> (manuel) : Affiche le manuel de la commande spécifiée
- # #Recherche
  collapsed:: true
	- [find](https://www.geeksforgeeks.org/find-command-in-linux-with-examples/) **<base> <paramètre> <fichier>** : Recherche un fichier par nom, type ou autre
	- [grep](https://www.geeksforgeeks.org/grep-command-in-unixlinux/) **<option> pattern <fichier>** : Recherche un ensemble de charactères dans un fichier donné
	- [history](https://www.geeksforgeeks.org/history-command-in-linux-with-examples/) **<option>** : affiche l'historique des commande précédemment exécutées
	- [locate](https://www.geeksforgeeks.org/locate-command-in-linux-with-examples/) **<fichier>** : Localise n'importe quel fichier ou répertoire sur le système. Utilise le fichier mlocate.db mis à jour toutes les 24h, qui indexe tous les fichiers du système
		- Possible de forcer la mise à jour : **sudo ubdatedb**
	- [whereis](https://en.wikibooks.org/wiki/Guide_to_Unix/Commands/Finding_Files#whereis) **<commande>** : Rechercher  les fichiers exécutables, les sources et les pages de manuel d'une commande
- # #[[I-O]]
  collapsed:: true
	- ## Périphériques audio
	  collapsed:: true
		- ### Pipewire / Wireplumber
		  collapsed:: true
			- #### Afficher les périphériques
			  collapsed:: true
				- ```shell
				  wpctl status
				  ```
				- **Sinks**: périphériques de sortie (enceintes, casques)
				- **Sources**: périphériques d'entrée (microphones)
			- #### Définir un périphérique de sortie par défaut
			  collapsed:: true
				- ```shell
				  wpctl set-default <ID> # ID: numéro du périphérique
				  wpctl set-default $(wpctl status | grep "Nom périphérique" | grep "\d+" -Po | head -n 1) # Récupère l'ID via le nom du périphérique
				  ```
- # #[[Fichiers et répertoires]]
  collapsed:: true
	- ## Navigation
	  collapsed:: true
		- [cd](https://www.geeksforgeeks.org/cd-command-in-linux-with-examples/) -> `change directory` <répertoire> : Permet de se déplacer dans l'arborescence de fichiers
		- [pwd](https://www.geeksforgeeks.org/pwd-command-in-linux-with-examples/) `print working directory` **<option>** : Affiche le chemin absolu vers le répertoire courant
		- [ls](https://www.geeksforgeeks.org/ls-command-in-linux/) **<option> <fichier / répertoire>** : Liste les fichiers et répertoires
	- ## Modification
	  collapsed:: true
		- [mkdir](https://www.geeksforgeeks.org/mkdir-command-in-linux-with-examples/) -> `make directory` **<option> <répertoire>** : Crée un nouveau répertoire
		- [touch](https://www.geeksforgeeks.org/touch-command-in-linux-with-examples/) **<fichier>** : Crée un fichier
		- [cp](https://www.geeksforgeeks.org/cp-command-linux-examples/) **<option> <source> <destination>** : Copie des fichiers ou répertoires
		- [cut](https://www.geeksforgeeks.org/cut-command-linux-examples/) **<option> <fichier>** : Coupe un fichier ou une chaine de caractères selon un délimiteur, un nombre de caractères ou autre
		- [mv](https://www.geeksforgeeks.org/mv-command-linux-examples/) **<option> <source> <destination>** : Déplace ou renomme des fichiers ou répertoires
		- [rm](https://www.geeksforgeeks.org/rm-command-linux-examples/) **<option> <fichier>** : Supprime un ou plusieurs fichiers
	- ## Redirection
	  collapsed:: true
		- [cat](https://www.geeksforgeeks.org/cat-command-in-linux-with-examples/) -> `concatenate` **<option> <fichier>** : Affiche le contenu d'un fichier
		- [diff](https://www.geeksforgeeks.org/diff-command-linux-examples/) **<options> <fichier1> <fichier2>** : Affiche les différences de contenu entre deux fichiers
		- [sort](https://www.geeksforgeeks.org/sort-command-linuxunix-examples/) **<option> <entrée>** : Tri le contenu d'un fichier selon l'option utilisée
		- [uniq](https://www.geeksforgeeks.org/uniq-command-in-linux-with-examples/) **<option> <entrée<sortie>>** : Filtre les doublons
		- [wc](https://www.geeksforgeeks.org/wc-command-linux-examples/) -> `word count` **<option> <fichier>** : Compte le nombre de lignes / mots / caractères / octets d'un fichier
- # #[[Gestion des droits]]
  collapsed:: true
	- [chmod](https://www.geeksforgeeks.org/chmod-command-linux/) -> `change mode` **<option> <mode> <fichier / répertoire>** : Change le mode d'accès au fichier ou répertoire
	- [chown](https://www.geeksforgeeks.org/chown-command-in-linux-with-examples/) -> `change owner` **<option> <propriétaire / group> <fichier>** : Change le propriétaire du fichier
- # #[[Gestion des utilisateurs]]
  id:: 668d2260-0977-49ba-a543-1d5610274a5c
  collapsed:: true
	- ## Création
	  collapsed:: true
		- Créer un **nouvel utilisateur** (il faut éviter au maximum d'utiliser le **root**) et l'ajouter au groupe **wheel /sudo (sudoers)** 
		  ```shell
		  useradd -m <utilisateur> -g wheel # Changer 'wheel' par 'sudo' en fonction
		  ```
		- Définir un mot de passe pour le nouvel utilisateur 
		  ```shell
		  passwd <utilisateur>
		  ```
	- ## Sudoers
	  collapsed:: true
		- Dé-commenter la ligne concernant le groupe **wheel** pour donner au groupe des **droits admins** 
		  ```shell
		  vim /etc/sudoers
		  ```
- # #Archive
  collapsed:: true
	- ## TAR + GZ
	  collapsed:: true
		- [tar](https://www.geeksforgeeks.org/tar-command-linux-examples/) **<options> <fichier-archive> <fichiers>** : Création, lecture, modification et extraction d'archives compressées ou non
	- ## ZIP
	  collapsed:: true
		- [zip](https://www.geeksforgeeks.org/zip-command-in-linux-with-examples/) **<options> <fichier-archive> <fichiers>** : Compresse les fichiers mentionnés dans une archive zip
- # #Stockage
  collapsed:: true
	- [du](https://www.geeksforgeeks.org/du-command-linux/) -> `disk used` **<option> <fichier>** : Affiche l'espace disque pris par un fichier / répertoire donné
	- [fdisk](https://www.geeksforgeeks.org/fdisk-command-in-linux-with-examples/) -> `format disk` **<options> <appareil>** : Permet de manipuler des partitions
	- [mkfs](https://www.geeksforgeeks.org/mkfs-command-in-linux-with-examples/) -> `make file system` **<options> <partition>** : Crée une partition sur l'appareil spécifié, généralement un disque ou une clef usb. L'opération efface toutes information présente sur le disque
	- [<u>mount](https://www.geeksforgeeks.org/mount-command-in-linux-with-examples/) **<options> <type> <appareil> <répertoire>** : Permet de monter (mount) le une partition sur le système de fichiers du système, ou de la démonter (umount)
- # #Processus
  collapsed:: true
	- [ps](https://www.geeksforgeeks.org/ps-command-in-linux-with-examples/) -> `process status` **<options>** : Liste les processus en cours d'exécution
- # #Polices
  collapsed:: true
	- [fc-cache](https://www.geeksforgeeks.org/fc-cache-command-in-linux-with-examples/) -> `fontconfig cache` **<options>** : Scan les répertoires dédiés aux polices et génère le cache de police.