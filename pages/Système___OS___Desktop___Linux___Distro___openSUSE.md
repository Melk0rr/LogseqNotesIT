# Description
	- Distribution #Système/OS/Desktop/Linux créée en 1994 comprenant 2 branches
		- [openSUSE Tumbleweed](https://get.opensuse.org/tumbleweed/) : #Programmation/Dev/Publication/Rolling release
		- [openSUSE Leap](https://get.opensuse.org/leap/) : #Programmation/Dev/Publication/Standard release
	- ## Caractéristiques
	- |**Modèle**|Communautaire avec appui corpo|
	  |**Mise à jour**|Rolling release(Tumbleweed)[:br]Fixe(Leap)|
	  |**Public**|Intermédiaire|
	  |**Usage**|Personnel(Tumbleweed)[:br]Serveur(Leap)|
	  |**Famille**|SUSE|
	  |**Basé sur**|Indépendant|
	  |**Base de**|GeckoLinux|
	  |**Gestionnaire de paquets**|#Système/OS/Desktop/Linux/Distro/openSUSE/zypper|
	  |**Format de paquet**|#Système/Paquets/Format/RPM|
	  |**Installateur graphique**|OUI|
	  |**Approche infra**|Hybride (snapshots)|
	  |**Site web**|[opensuse.org](https://www.opensuse.org/)|
- # Installation
  collapsed:: true
	- ## Post-reboot
	  collapsed:: true
		- ### Configuration Zypper
		  collapsed:: true
			- ```shell
			  sudo vim /etc/zypp/zypp.conf
			  ```
			- ```vim
			  [main]
			  solver.dupAllowVendorChange=false
			  multiversion=provides:multiversion(kernel)
			  multiversion.kernels=latest,latest-1,running
			  repo.refresh.delay=1080
			  download.max_concurrent_connections=10
			  download.min_download_speed=20000
			  commit.downloadMode=DownloadInAdvance
			  ```
- # Post-installation
- # Maintenance