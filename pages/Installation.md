# #[[Common Linux]]
	- ## #Partitions
	  id:: 65c8ff54-db3b-48de-b9d4-ece65f422173
	  collapsed:: true
		- [efi](https://wiki.archlinux.org/title/EFI_system_partition) : partition dédiée au **chargeur d'amorçage** (*boot loader*).
			- Minimum **1Go** requis dans la plupart des cas surtout si plusieurs kernels utilisés
		- [swap](https://wiki.archlinux.org/title/swap) : espace ou fichier utilisé pour **étendre la mémoire physique**. Pour faire simple, si toute la mémoire RAM est utilisée, alors le système utilisera l'espace swap en attendant que la RAM ne se libère. Les opérations utilisant le swap sont bien plus **lentes** que lorsque le système utilise la mémoire vive.
			- Une partition swap n'est plus vraiment requise dans la mesure où les quantités de RAM sont généralement élevées.
			- Une partition swap est requise si le système est configuré pour de l'==hibernation==
			  id:: 65c8ff54-14ef-48dd-8926-c07e0b1ca4f6
				- RAM **16Go** : ~~hibernation~~ => **4Go** / *hibernation* => **20Go**
				- RAM **32Go** : ~~hibernation~~ => **6Go** / *hibernation* => **38Go**
				- RAM **64Go** : ~~hibernation~~ => **8Go** / *hibernation* => **72Go**
		- [root (/)](https://wiki.archlinux.org/title/Partitioning#/) : partition racine qui accueille le système de fichiers
		- [home (/home)](https://wiki.archlinux.org/title/Partitioning#/) : répertoire contenant les fichiers utilisateurs
- # [Arch Linux](((65c8ff54-d1f3-41db-9746-5d11eec23b84)))
	- #Drivers
		- #Imprimante
		  collapsed:: true
			- #Paquets
			  collapsed:: true
				- ghostscript
				- gsfonts
				- [cups](https://wiki.archlinux.org/title/CUPS_(Fran%C3%A7ais)) -> `Common UNIX Printing System`
				- cups-filters
				- cups-pdf
				- system-config-printer
				- avahi
				- foomatic-db-engine
				- [foomatic-db](https://wiki.archlinux.org/title/CUPS#Foomatic)
				- foomatic-db-ppds
				- foomatic-db-nonfree
				- foomatic-db-nonfree-ppds
				- gutenprint
				- foomatic-db-gutenprint-ppds
			- #Paquets Epson
				- epson-inkjet-printer-escpr
				- epson-inkjet-printer-escpr2
			- #Paquets HP
				- hplip
				- python-pyqt5
			- **Démarrage**
				- `sudo systemctl enable --now avahi-daemon`
				- `sudo systemctl enable --now cups`
		- #Bluetooth
		  collapsed:: true
			- #Paquets
				- bluez
				- bluez-plugins
				- bluez-utils
			- Démarrage
				- `sudo systemctl enable --now bluetooth`
		- #Graphique
		  collapsed:: true
			- #AMD
			  collapsed:: true
				- #Paquets
				  collapsed:: true
					- mesa
					- lib32-mesa
					- vulkan-radeon
					- lib32-vulkan-radeon
					- vulkan-icd-loader
					- lib32-vulkan-icd-loader
					- vulkan-mesa-layers
					- lib32-vulkan-mesa-layers
					- libva-mesa-driver
					- lib32-libva-mesa-driver
					- mesa-vdpau
					- lib32-mesa-vdpau
	- #[[Desktop Environment]]
		- #Hyprland
		  collapsed:: true
			- #Paquets
				- cliphist
				- curl
				- dunst
				- grim
				- gvfs
				- gvfs-mtp
				- imagemagick
				- jq
				- kitty
				- kvantum
				- nano
				- network-manager-applet
				- pamixer
				- pavucontrol
				- pipewire-alsa
				- playerctl
				- polkit-gnome
				- python-requests
				- python-pywal
				- qt5ct
				- qt6ct
				- qt6-svg
				- rofi-lbonn-wayland-git
				- slurp
				- swappy
				- swayidle
				- swaylock-effects-git
				  id:: 65cfcd67-7ed8-4880-ad65-3224c06937a6
				- swww
				- waybar
				- wget
				- wl-clipboard
				- wlogout
				- xdg-user-dirs
				- yad
-
-