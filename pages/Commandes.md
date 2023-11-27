- #Linux
	- #[[Common Linux]]
		- #Documentation
		  collapsed:: true
			- [Documentation en ligne](https://www.geeksforgeeks.org/linux-commands/)
			  id:: 65217c2c-e35f-404b-91ad-66bac8c07a1d
			- [man](https://www.geeksforgeeks.org/man-command-in-linux-with-examples/) <commande> (manuel) : Affiche le manuel de la commande spécifiée
		- #Recherche
		  collapsed:: true
			- [find](https://www.geeksforgeeks.org/find-command-in-linux-with-examples/) **<base> <paramètre> <fichier>** : Recherche un fichier par nom, type ou autre
			- [grep](https://www.geeksforgeeks.org/grep-command-in-unixlinux/) **<option> pattern <fichier>** : Recherche un ensemble de charactères dans un fichier donné
			- [history](https://www.geeksforgeeks.org/history-command-in-linux-with-examples/) **<option>** : affiche l'historique des commande précédemment exécutées
			- [locate](https://www.geeksforgeeks.org/locate-command-in-linux-with-examples/) **<fichier>** : Localise n'importe quel fichier ou répertoire sur le système. Utilise le fichier mlocate.db mis à jour toutes les 24h, qui indexe tous les fichiers du système
				- Possible de forcer la mise à jour : **sudo ubdatedb**
			- [whereis](https://en.wikibooks.org/wiki/Guide_to_Unix/Commands/Finding_Files#whereis) **<commande>** : Rechercher  les fichiers exécutables, les sources et les pages de manuel d'une commande
		- #[[Manipulation de fichiers et répertoires]]
		  collapsed:: true
			- [cat](https://www.geeksforgeeks.org/cat-command-in-linux-with-examples/) -> `concatenate` **<option> <fichier>** : Affiche le contenu d'un fichier
			- [cd](https://www.geeksforgeeks.org/cd-command-in-linux-with-examples/) -> `change directory` <répertoire> : Permet de se déplacer dans l'arborescence de fichiers
			- [cp](https://www.geeksforgeeks.org/cp-command-linux-examples/) **<option> <source> <destination>** : Copie des fichiers ou répertoires
			- [cut](https://www.geeksforgeeks.org/cut-command-linux-examples/) **<option> <fichier>** : Coupe un fichier ou une chaine de caractères selon un délimiteur, un nombre de caractères ou autre
			- [diff](https://www.geeksforgeeks.org/diff-command-linux-examples/) **<options> <fichier1> <fichier2>** : Affiche les différences de contenu entre deux fichiers
			- [ls](https://www.geeksforgeeks.org/ls-command-in-linux/) **<option> <fichier / répertoire>** : Liste les fichiers et répertoires
			- [mkdir](https://www.geeksforgeeks.org/mkdir-command-in-linux-with-examples/) -> `make directory` **<option> <répertoire>** : Crée un nouveau répertoire
			- [mv](https://www.geeksforgeeks.org/mv-command-linux-examples/) **<option> <source> <destination>** : Déplace ou renomme des fichiers ou répertoires
			- [pwd](https://www.geeksforgeeks.org/pwd-command-in-linux-with-examples/) `print working directory` **<option>** : Affiche le chemin absolu vers le répertoire courant
			- [rm](https://www.geeksforgeeks.org/rm-command-linux-examples/) **<option> <fichier>** : Supprime un ou plusieurs fichiers
			- [sort](https://www.geeksforgeeks.org/sort-command-linuxunix-examples/) **<option> <entrée>** : Tri le contenu d'un fichier selon l'option utilisée
			- [touch](https://www.geeksforgeeks.org/touch-command-in-linux-with-examples/) **<fichier>** : Crée un fichier
			- [uniq](https://www.geeksforgeeks.org/uniq-command-in-linux-with-examples/) **<option> <entrée<sortie>>** : Filtre les doublons
			- [wc](https://www.geeksforgeeks.org/wc-command-linux-examples/) -> `word count` **<option> <fichier>** : Compte le nombre de lignes / mots / caractères / octets d'un fichier
		- #[[Gestion des droits]]
		  collapsed:: true
			- [chmod](https://www.geeksforgeeks.org/chmod-command-linux/) -> `change mode` **<option> <mode> <fichier / répertoire>** : Change le mode d'accès au fichier ou répertoire
			- [chown](https://www.geeksforgeeks.org/chown-command-in-linux-with-examples/) -> `change owner` **<option> <propriétaire / group> <fichier>** : Change le propriétaire du fichier
		- #Archive
		  collapsed:: true
			- [tar](https://www.geeksforgeeks.org/tar-command-linux-examples/) **<options> <fichier-archive> <fichiers>** : Création, lecture, modification et extraction d'archives compressées ou non
			- [zip](https://www.geeksforgeeks.org/zip-command-in-linux-with-examples/) **<options> <fichier-archive> <fichiers>** : Compresse les fichiers mentionnés dans une archive zip
		- #Stockage
		  collapsed:: true
			- [du](https://www.geeksforgeeks.org/du-command-linux/) -> `disk used` **<option> <fichier>** : Affiche l'espace disque pris par un fichier / répertoire donné
			- [fdisk](https://www.geeksforgeeks.org/fdisk-command-in-linux-with-examples/) -> `format disk` **<options> <appareil>** : Permet de manipuler des partitions
			- [mkfs](https://www.geeksforgeeks.org/mkfs-command-in-linux-with-examples/) -> `make file system` **<options> <partition>** : Crée une partition sur l'appareil spécifié, généralement un disque ou une clef usb. L'opération efface toutes information présente sur le disque
			- [<u>mount](https://www.geeksforgeeks.org/mount-command-in-linux-with-examples/) **<options> <type> <appareil> <répertoire>** : Permet de monter (mount) le une partition sur le système de fichiers du système, ou de la démonter (umount)
		- #Processus
		  collapsed:: true
			- [ps](https://www.geeksforgeeks.org/ps-command-in-linux-with-examples/) -> `process status` **<options>** : Liste les processus en cours d'exécution
	- #[[Arch Linux]]
		- #[[Gestion de paquets]]
			- [downgrade](https://github.com/archlinux-downgrade/downgrade) **<options> <pkg>** : Rétrograde la version du paquet spécifié
				- Nécessite le paquet **downgrade** -> `yay -S downgrade`
				- [Rétrograder via pacman](https://wiki.archlinux.org/title/downgrading_packages)
-
- #Windows
	- #[[Gestion des droits]]
	  collapsed:: true
		- [Get-Acl](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-acl?view=powershell-7.3) **<option> <fichier / répertoire>** : Retourne la description de sécurité pour un fichier ou répertoire
	- #[[Gestion de mots de passe]]
	  collapsed:: true
		- [ConvertFrom-SecureString](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/convertfrom-securestring?view=powershell-7.3) **<chaîne> <options>** : convertit une chaîne sécurisée en chaîne chiffrée standard
			- `"P@ssword1" | ConvertTo-SecureString -AsPlainText | ConvertFrom-SecureString | Out-File "C:\Temp\password"`
		- [ConvertTo-SecureString](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/convertto-securestring?view=powershell-7.3) **<chaîne> <options>** : convertit une chaîne de caractères en chaîne sécurisée
			- `"P@ssword1" | ConvertTo-SecureString -AsPlainText`
			- `Get-Content "C:\Temp\password" | ConvertTo-SecureString`