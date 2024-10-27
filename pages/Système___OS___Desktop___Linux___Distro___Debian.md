-
- # Description
	- Distribution #Système/OS/Desktop/Linux créée en 1993
	- ## Caractéristiques
		- |**Modèle**|Communautaire|
		  |**Mise à jour**|Fixe|
		  |**Public**|Intermédiaire / Expérimenté|
		  |**Usage**|Personnel[:br]Serveur|
		  |**Famille**|Debian|
		  |**Basé sur**|Indépendant|
		  |**Base de**|#Système/OS/Desktop/Linux/Distro/Debian/Ubuntu, #Système/OS/Desktop/Linux/Distro/Debian/Sec/Kali, #Système/OS/Desktop/Linux/Distro/Debian/Sec/Parrot, #[[Système/OS/Desktop/Linux/Distro/Debian/Linux Mint]], Rasberry Pi OS|
		  |**Gestionnaire de paquets**|#Système/OS/Desktop/Linux/Distro/Debian/apt|
		  |**Format de paquet**|#Système/Paquets/Format/DEB|
		  |**Installateur graphique**|OUI|
		  |**Approche infra**|Traditionnelle|
		  |**Site web**|[debian.org](https://www.debian.org/)|
- # Installation
  collapsed:: true
	- ## Post-reboot
	  collapsed:: true
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
					- **deb**: fichiers **binaires** #Système/Paquets/Format/DEB précompilés
					- **deb-src**: paquets **sources**
				- **URL** du #Système/Paquets/Mirroirs
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
		- ### #Sécurité/Offensif/Pentest/Bruteforce
			- #### #Système/Paquets
				- ```shell
				  sudo apt install hydra wfuzz
				  ```
		- ### #Sécurité/Défensif/Forensic
			- #### #Système/Paquets
				- ```shell
				  sudo apt install autopsy
				  ```
		- ### #Sécurité/Offensif/Scan
			- #### #Système/Paquets
				- ```shell
				  sudo apt install nesuss nmap wireshark
				  ```
		- ### Usurpation d'identité
			- #### #Système/Paquets
				- ```shell
				  sudo apt install macchanger
				  ```
		- ### ONE-LINER
			- ```shell
			  sudo apt install hydra wfuzz autopsy nessus nmap wireshark macchanger # Paquets
			  sudo git clone https://github.com/scipag/vulscan /usr/share/nmap/scripts/vulscan # Vulnerability scan script for nmap
			  ```
- # Maintenance
-