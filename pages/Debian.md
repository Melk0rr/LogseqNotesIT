# Description
	- Distribution #Linux créée en 1993
	- ## Caractéristiques
	  collapsed:: true
		- |**Modèle**|Communautaire|
		  |**Mise à jour**|Fixe|
		  |**Public**|Intermédiaire / Expérimenté|
		  |**Usage**|Personnel[:br]Serveur|
		  |**Famille**|Debian|
		  |**Basé sur**|Indépendant|
		  |**Base de**|#Ubuntu, Kali, Parrot, #Mint, Rasberry Pi OS|
		  |**Gestionnaire de paquets**|#apt|
		  |**Format de paquet**|#DEB|
		  |**Installateur graphique**|OUI|
		  |**Approche infra**|Traditionnelle|
		  |**Site web**|[debian.org](https://www.debian.org/)|
- # Installation
	- ## Post-reboot
		- ### Sources
		  collapsed:: true
			- #### Changer la liste des sources
				- ```shell
				  sudo vim /etc/apt/sources.list
				  ```
			- #### Format des sources:
				- ```vim
				  deb http://debian.mirror.com/debian/ distribution composant1 composant2 composant3
				  deb-src http://debian.mirror.com/debian/ distribution composant1 composant2 composant3
				  ```
				- **Type d'archive**
				  logseq.order-list-type:: number
					- **deb**: fichiers **binaires** #DEB précompilés
					- **deb-src**: paquets **sources**
				- **URL** du #Mirroirs
				  logseq.order-list-type:: number
				- **Distribution**
				  logseq.order-list-type:: number
					- **Nom de code** de la *prochaine version stable*.
						- stretch
						- buster
						- bullseye
						- bookworm
						- sid
					- **Classe** de paquets  souhaitée (+ ou - **stable**).
						- oldoldstable
						- oldstable
						- stable
						- testing
						- unstable
				- **Composants**:
				  logseq.order-list-type:: number
					- [main](https://www.debian.org/doc/debian-policy/ch-archive#s-main): paquets **officiels** de la distribution
					- [contrib](https://www.debian.org/doc/debian-policy/ch-archive#s-contrib): paquets qui respectent la politique [DFSG](https://www.debian.org/social_contract#guidelines) de debian mais qui ont des dépendances **hors de main**
					- [non-free](https://www.debian.org/doc/debian-policy/ch-archive#s-non-free): paquets qui ne **respectent pas** la politique DFSG de debian
- # Post-installation
	- ## #Sécurité
		- ### #Bruteforce
			- #### #Paquets
				- ```shell
				  sudo apt install hydra
				  ```
		- ### #Forensic
			- #### #Paquets
				- ```shell
				  sudo apt install autopsy
				  ```
		- ### #Scans
			- #### #Paquets
				- ```shell
				  sudo apt install nesuss nmap wireshark
				  ```
		- ### Usurpation d'identité
			- #### #Paquets
				- ```shell
				  sudo apt install macchanger
				  ```
- # Maintenance