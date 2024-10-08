# Général
	- [flatpak](https://flatpak.org/) : Gestionnaire de #Paquets multi distributions offrant un environnement sandbox. Flatpak permet notamment de disposer de certains paquets dans leurs versions plus `rolling` tout en conservant une base plus stable. C'est notamment le cas en associant flatpak avec Debian ou avec apt en général.
- # Base #Debian
	- #apt : Gestionnaire de #Paquets développé en #C++ et commun aux distributions basées sur #Debian
	- ### Wrapper
	  collapsed:: true
		- [nala](https://gitlab.com/volian/nala) : wrapper #apt développé en #Python avec quelques fonctionnalités clefs
			- **Lisibilité** accrue
			- **Téléchargements parallèles de 3 paquets** maximum (pour limiter l'impact sur les dépôts)
			- **Gestion des mirroirs**
			- **Historique des commandes**
- # Base #[[Arch Linux]]
	- #pacman : Gestionnaire de #Paquets développé en #C spécifique à #[[Arch Linux]]
	- ### #[[AUR helper]]
	  collapsed:: true
		- [paru](https://github.com/Morganamilo/paru) : Gestionnaire de #Paquets pour AUR sur #[[Arch Linux]] ( écrit en #Rust )
		  id:: 657ac02b-fd09-4dbd-ac7b-862e422ee55a
		- [yay](https://github.com/Jguer/yay) : Gestionnaire de #Paquets pour AUR sur #[[Arch Linux]] ( écrit en #Go )
		  id:: 654cd0e6-59fd-492f-9c7a-3300b72b7da2
- # Base #openSUSE
	- [zypper](https://en.opensuse.org/Portal:Zypper) : Gestionnaire de #Paquets développé en #C++ et spécifique à #openSUSE