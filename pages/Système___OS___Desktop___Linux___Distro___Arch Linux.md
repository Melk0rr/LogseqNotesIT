# Description
	- Distribution #Système/OS/Desktop/Linux créée en 2002 par Judd Vinet. Elle suit le principe **KISS**: Keep It Simple, Stupid
	- ## Caractéristiques
		- |**Modèle**|Communautaire|
		  |**Mise à jour**|Rolling release|
		  |**Public**|Expérimenté|
		  |**Usage**|Personnel|
		  |**Famille**|Arch Linux|
		  |**Basé sur**|Indépendant|
		  |**Base de**|BlackArch, EndeavourOS, Manjaro, CachyOS|
		  |**Gestionnaire de paquets**|#[[Système/OS/Desktop/Linux/Distro/Arch Linux/pacman]]|
		  |**Format de paquet**|#Système/Paquets/Format/PKG [:br]TAR.ZST|
		  |**Installateur graphique**|NON|
		  |**Approche infra**|Traditionnelle|
		  |**Site web**|[archlinux.org](http://archlinux.org)|
- # Installation
  id:: 65c8ff54-d1f3-41db-9746-5d11eec23b84
	- [Guide officiel](https://wiki.archlinux.org/title/Installation_guide_(Fran%C3%A7ais))
	  id:: 65c93b3e-72e6-4c5a-94e6-6528aba7488e
	- ## Base
		- ### Disposition clavier
		  collapsed:: true
			- Changer la configuration du clavier. Utile surtout pour les claviers non QWERTY 
			  logseq.order-list-type:: number
			  ```shell
			  loadkeys fr
			  ```
		- ### Connexion à internet
			- Vérifier la connectivité internet. Mieux vaut une connexion ethernet pour se faciliter la vie 
			  logseq.order-list-type:: number
			  ```shell
			  ping archlinux.org
			  ```
			- #### #[[Réseau/Sans-fil/WiFi]]
			  collapsed:: true
				- ```shell
				  # Entrer dans le mode interactif de l'utilitaire de controle sans fil
				  iwctl
				  
				  # Lister les interfaces WiFi
				  device list
				  
				  # Lister les réseaux disponibles
				  station wlan0 get-networks
				  
				  # Connexion à un réseau wifi
				  station wlan0 connect <network>
				  ```
		- ### Check UEFI
		  collapsed:: true
			- S'assurer que l'installation est bien en mode **UEFI** (sauf si BIOS souhaité). Si la commande ne retourne rien: l'installation est en mode BIOS
			  ```shell
			  ls /sys/firmware/efi/efivars
			  ```
		- ### Horloge
		  collapsed:: true
			- Pour vérifier que la date est bien valide 
			  logseq.order-list-type:: number
			  ```shell
			  # Vérificaiton
			  timedatectl
			  
			  # Activation du NTP
			  timedatectl set-ntp true
			  ```
		- ### Partitionnement
		  collapsed:: true
			- Afficher les disques et partitions actuelles (*blocs*) -> identifier le disque sur lequel installer le système 
			  logseq.order-list-type:: number
			  ```shell
			  lsblk
			  ```
			- Vérifier que la table de partition est bien en GPT 
			  logseq.order-list-type:: number
			  ```shell
			  # Lister les propriétés du disque : le label doit être "gpt"
			  fdisk -l <disque>
			  
			  # Si la partition n'est pas en GPT
			  fdisk
			  
			  # Créer une table GPT avec l'option 'g'
			  ```
			- Exécuter l'utilitaire [cfdisk](https://www.geeksforgeeks.org/cfdisk-command-in-linux-with-examples/) pour créer des partitions sur le disque sélectionné (e.g. nvme0n1) 
			  logseq.order-list-type:: number
			  collapsed:: true
			  ```shell
			  # Lancer CFDISK
			  cfdisk <disque>
			  ```
				- Dans la plupart des cas on veut une table de #Système/Partitions **GPT**
				  logseq.order-list-type:: number
				- Si cfdisk ne demande pas le type souhaité -> s'assurer que le label **gpt** est présent
				  logseq.order-list-type:: number
				- Sinon ajouter le label manuellement avec [fdisk](https://www.geeksforgeeks.org/fdisk-command-in-linux-with-examples/)
				  logseq.order-list-type:: number
				- Partitionner le disque (c.f. ((65c8ff54-db3b-48de-b9d4-ece65f422173)))
				  logseq.order-list-type:: number
				- Quitter une fois les changements écrits
				  logseq.order-list-type:: number
		- ### Formatage
		  collapsed:: true
			- Pour l'exemple : <**disque**><*partition* x> => **nvme0n1***px*
			- Pour vérifier les changements: 
			  logseq.order-list-type:: number
			  ```shell
			  lsblk
			  ```
			- Formater la partition **efi** en **FAT32** (pour la compatibilité): 
			  logseq.order-list-type:: number
			  ```shell
			  mkfs.fat -F 32 /dev/nvme0n1p1
			  ```
			- "Formater" la partition **swap**, (pas de formatage à proprement parlé) et l'activer: 
			  logseq.order-list-type:: number
			  ```shell
			  mkswap /dev/nvme0n1p2
			  swapon /dev/nvme0n1p2
			  ```
			- Formater la partition **racine (/)** en **EXT4** (ou **BTRFS**, **NFS**, etc) et la partition **home**: 
			  logseq.order-list-type:: number
			  ```shell
			  mkfs.ext4 /dev/nvme0n1p3
			  mkfs.ext4 /dev/nvme0n1p4
			  ```
			- Attribuer un label à chaque partition 
			  logseq.order-list-type:: number
			  ```shell
			  # Pour une partition EXT
			  e2label /dev/XXX "new label" # ext2/3/4
			  
			   # Pour une partition BTRFS
			  btrfs filesystem label /dev/XXX "new label"
			  ```
		- ### Montage des partitions
		  collapsed:: true
			- **Monter** la partition **racine** sur **/mnt** 
			  logseq.order-list-type:: number
			  ```shell
			  mount /dev/nvme0n1p3 /mnt
			  ```
			- Créer les répertoires **boot** et **home** qui serviront à monter nos autres partitions 
			  logseq.order-list-type:: number
			  ```shell
			  mkdir /mnt/{boot,home}
			  ```
			- **Monter** la partition **boot** sur **/mnt/boot**. Si en mode **UEFI** possible de monter sur **/efi** 
			  logseq.order-list-type:: number
			  ```shell
			  mount /dev/nvme0n1p1 /mnt/boot
			  ```
			- **Monter** la partition **home** sur **/mnt/home** 
			  logseq.order-list-type:: number
			  id:: 65cfcd67-0d1a-4a0f-980a-7163829f7f5c
			  ```shell
			  mount /dev/nvme0n1p4 /mnt/home
			  ```
	- ## Installation
	  collapsed:: true
		- ### Mirroirs
		  id:: 65c92958-d6c2-4ea2-9cf7-d9d7ad35e33b
		  collapsed:: true
			- Sélectionner les meilleurs miroirs 
			  logseq.order-list-type:: number
			  ```shell
			  reflector --country France --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
			  ```
			- Dé-commenter la section **multilib** 
			  logseq.order-list-type:: number
			  ```shell
			  vim /etc/pacman.conf
			  ```
		- ### Installation des #Système/Paquets essentiels
		  collapsed:: true
			- Installer le système et quelques paquets essentiels 
			  logseq.order-list-type:: number
			  ```shell
			  pacstrap /mnt base base-devel linux linux-headers linux-firmware pacman-contrib
			  ```
				- **base** : installation minimale d'Arch linux
				  logseq.order-list-type:: number
				- **linux** : noyau linux
				  logseq.order-list-type:: number
				- **linux-firmware** : firmware utiles pour certains composants matériel (clavier, souris, etc.)
				  logseq.order-list-type:: number
				- **pacman-contrib** : utilitaire pour le maintien de Arch
				  logseq.order-list-type:: number
				- **networkmanager** : utilitaire de configuration et gestion réseau
				  logseq.order-list-type:: number
				- **firewalld** : utilitaire firewall
				  logseq.order-list-type:: number
			- Installer des paquets relatifs au **boot** 
			  logseq.order-list-type:: number
			  ```shell
			  pacstrap /mnt efibootmgr os-prober
			  ```
			- Quelques paquets de manipulation de divers **systèmes de fichiers** 
			  logseq.order-list-type:: number
			  ```shell
			  pacstrap /mnt ntfs-3g exfat-utils mtools dosfstools
			  ```
			- Installer les pages de **manuels** 
			  logseq.order-list-type:: number
			  ```shell
			  pacstrap /mnt man-db man-pages
			  ```
			- Installer les paquets pour la gestion du **son**
			  logseq.order-list-type:: number
			  ```shell
			  pacstrap /mnt pipewire pipewire-jack pipewire-pulse pipewire-alsa wireplumber lib32-pipewire alsa-utils alsa-plugins alsa-firmware alsa-ucm-conf sof-firmware
			  ```
		- ### Configuration système
		  collapsed:: true
			- Générer le fichier fstab -> indique les **points de montage** 
			  logseq.order-list-type:: number
			  ```shell
			  genfstab -U /mnt >> /mnt/etc/fstab
			  ```
			  
			  ```vim
			  # <device>                                <dir> <type> <options> <dump> <fsck>
			  UUID=0a3407de-014b-458b-b5c1-848e92a327a3 /     ext4   defaults  0      1
			  UUID=f9fe0b69-a280-415d-a03a-a32752370dee none  swap   defaults  0      0
			  UUID=b411dc99-f0a0-4c87-9e05-184977be8539 /home ext4   defaults  0      2
			  ```
			- Basculer sur le point de montage **racine** 
			  logseq.order-list-type:: number
			  ```shell
			  arch-chroot /mnt
			  ```
			- Définir le **nom de la machine** sur le réseau 
			  logseq.order-list-type:: number
			  ```shell
			  vim /etc/hostname
			  ```
			- Définir la table locale 
			  logseq.order-list-type:: number
			  ```shell
			  vim /etc/hosts
			  ```
				- ```vim
				  127.0.0.1  localhost
				  ::1  localhost
				  127.0.0.1  <hostname>.localdomain <hostname>
				  ```
			- Définir la **disposition clavier** et la **police** 
			  logseq.order-list-type:: number
			  ```shell
			  vim /etc/vconsole.conf
			  ```
				- ```vim
				  KEYMAP=fr-latin9
				  FONT=eurlatgr
				  ```
			- Définir les **locales** 
			  logseq.order-list-type:: number
			  ```shell
			  vim /etc/locale.conf
			  ```
				- ```vim
				  LANG=fr_FR.UTF-8
				  ```
			- **Dé-commenter** les langues souhaitées 
			  logseq.order-list-type:: number
			  ```shell
			  vim /etc/locale.gen
			  ```
			- **Générer les locales** 
			  logseq.order-list-type:: number
			  ```shell
			  locale-gen
			  ```
			- Créer un lien symbolique pour **définir le fuseau horaire** 
			  logseq.order-list-type:: number
			  ```shell
			  ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime
			  ```
			- Ajuster l'**horloge** 
			  logseq.order-list-type:: number
			  ```shell
			  hwclock --systohc
			  ```
			- Pas nécessaire en théorie si le kernel a bien été installé directement avec **pacstrap** 
			  logseq.order-list-type:: number
			  ```shell
			  mkinitcpio -P
			  ```
		- ### Installation chargeur d'amorçage
		  collapsed:: true
			- #### systemd-boot
				- Installer systemd-boot 
				  logseq.order-list-type:: number
				  ```shell
				  bootctl --path=/boot install
				  ```
					- Si l'installateur affiche une erreur concernant un problème de permissions
					  logseq.order-list-type:: number
						- S'assurer que la partition efi comporte *fmask=0137,dmask=0027*
						  ```shell
						  vim /etc/fstab
						  umount /boot
						  mount /boot
						  bootctl update
						  ```
		- ### Derniers ajustements avant reboot
		  collapsed:: true
			- Ajouter *default arch.conf* pour définir une option par défaut (possible d'ajuster le **timeout** de démarrage) 
			  logseq.order-list-type:: number
			  ```shell
			  vim /boot/loader/loader.conf
			  ```
			- Ajouter les lignes sivantes (**Attention à la casse**)
			  logseq.order-list-type:: number
			  ```shell
			  vim /boot/loader/entries/arch.conf
			  ```
				- ```vim
				  title   Arch Linux
				  linux   /vmlinuz-linux
				  initrd  /initramfs-linux.img
				  options root=/dev/nvme0n1p3 rw
				  ```
				- Pour des raisons de sécurité, il vaut mieux utiliser l'**UUID** de la partition *root*options
					- ```shell
					  # Afficher l'UUID de la partition
					  blkid /dev/<partition_root>
					  
					  # Copier / Coller l'UUID (pas la PARTUUID)
					  
					  # Ou rediriger directement
					  blkid /dev/<partition_root> >> /boot/loader/entries/arch.conf
					  ```
					- ```vim
					  options root="UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" rw
					  ```
			- Activer le gestionnaire réseau pour le redémarrage 
			  logseq.order-list-type:: number
			  ```shell
			  systemctl enable --now NetworkManager
			  ```
			- Installation des mises à jour **microcode**
			  logseq.order-list-type:: number
			  ```shell
			  # AMD
			  pacman -Syu amd-ucode
			  
			  # Intel
			  pacman -Syu intel-ucode
			  ```
			- ==Définir le mot de passe root==
			  logseq.order-list-type:: number
			  ```shell
			  passwd root
			  ```
			  Si oubli :
				- Redémarrer la machine et **booter sur média d'installation**
				  logseq.order-list-type:: number
				- Monter la partition **racine** 
				  logseq.order-list-type:: number
				  ```shell
				  mount /dev/nvme0n1p3 /mnt
				  ```
				- Basculer sur le système 
				  logseq.order-list-type:: number
				  ```shell
				  arch-chroot /mnt
				  ```
				- Définir le mot de passe 
				  logseq.order-list-type:: number
				  ```shell
				  passwd root
				  ```
				- Suivre à nouveau les étapes **ci-après**
				  logseq.order-list-type:: number
			- Revenir sur le **système temporaire** 
			  logseq.order-list-type:: number
			  ```shell
			  exit
			  ```
			- Démonter tout le contenu de **/mnt** puis redémarrer 
			  logseq.order-list-type:: number
			  ```shell
			  umount -R /mnt
			  reboot
			  ```
	- ## Post-reboot
		- ### #Système/Paquets/Mirroirs
		  collapsed:: true
			- ((65c92958-d6c2-4ea2-9cf7-d9d7ad35e33b)) + dé-commenter également les lignes suivantes
			  logseq.order-list-type:: number
			  ```
			  Color
			  VerbosePkgLists
			  ParallelDownloads = 5
			  ```
		- ### [Utilisateurs](((668d2260-0977-49ba-a543-1d5610274a5c)))
		- ### #[[Réseau/Sans-fil/WiFi]]
		  collapsed:: true
			- Pour se connecter en Wifi sur notre nouvelle installation 
			  ```shell
			  # S'assurer que NetworkManager soit bien activé
			  sudo systemctl enable --now NetworkManager
			  
			  # Lister les interfaces
			  nmcli d
			  
			  # Activer le wifi
			  nmcli r wifi on
			  
			  # Lister les réseaux disponibles
			  nmcli d wifi list
			  
			  # Connexion à un ssid
			  nmcli d wifi connect <ssid> -ask
			  ```
		- ### #[[Système/OS/Desktop/Linux/Distro/Arch Linux/AUR helper]]
		  collapsed:: true
			- #### [Yay]([yay](https://github.com/Jguer/yay) : Gestionnaire de #Système/Paquets pour AUR sur #[[Système/OS/Desktop/Linux/Arch Linux ]] ( écrit en #Programmation/Langage/Go ))
				- logseq.order-list-type:: number
				  ```shell
				  sudo pacman -S --needed git base-devel
				  git clone https://aur.archlinux.org/yay.git
				  cd yay-bin
				  makepkg -si
				  ```
				- Support mises à jour git 
				  logseq.order-list-type:: number
				  ```shell
				  yay -Y --gendb
				  yay -Y --devel --save
				  ```
			- #### [Paru]([paru](https://github.com/Morganamilo/paru) : Gestionnaire de #Système/Paquets pour AUR sur #[[Système/OS/Desktop/Linux/Distro/Arch Linux]] ( écrit en #Programmation/Langage/Rust ))
- # Post-installation
  collapsed:: true
	- ## #[[Hardware/Contrôle]]
	  collapsed:: true
		- ### #Hardware/Driver/AMD
		  collapsed:: true
			- ```shell
			  # Défaut
			  sudo pacman -S --needed mesa-git lib32-mesa vulkan-radeon vulkan-icd-loader lib32-vulkan-icd-loader
			  
			  # Mesa TKG
			  git clone https://github.com/Frogging-Family/mesa-git
			  cd mesa-tkg
			  makepkg -si
			  ```
			- ==Ne pas installer== **amdvlk** ou **lib32-amdvlk** : ces paquets s'imposent comme paquets par défaut et peuvent causer beaucoup de problèmes
			- #### #Système/Paquets
				- [mesa](https://www.mesa3d.org/)
				- [mesa-tkg](https://github.com/Frogging-Family/mesa-git) : version maintenue par **TKG** -> contient des patchs et fixes supplémentaires
		- ### #Hardware/Contrôle/Affichage
		  collapsed:: true
			- ```shell
			  yay -S ddcutil
			  ```
		- ### #Hardware/Contrôle/Impression
		  collapsed:: true
			- ```shell
			  # Général
			  yay -S ghostscript gsfonts cups cups-filters cups-pdf system-config-printer avahi foomatic-db-engine foomatic-db foomatic-db-ppds foomatic-db-nonfree foomatic-db-nonfree-ppds gutenprint foomatic-db-gutenprint-ppds
			  
			  # Activation des daemon
			  sudo systemctl enable --now avahi-daemon
			  sudo systemctl enable --now cups
			  
			  # Epson
			  yay -S epson-inkjet-printer-escpr epson-inkjet-printer-escpr2
			  
			  # HP
			  yay -S hplip
			  ```
			- ### #Système/Paquets
				- [CUPS](https://openprinting.github.io/cups/)
				- [avahi](https://github.com/avahi/avahi)
		- ### #Réseau/Sans-fil/Bluetooth
		  collapsed:: true
			- ```shell
			  yay -S bluez bluez-plugins bluez-utils
			  sudo systemctl enable --now bluetooth
			  ```
			- ### #Système/Paquets
				- [bluez](https://www.bluez.org/)
	- ## #[[Système/OS/FS]]
	  collapsed:: true
		- ### Nettoyage
		  collapsed:: true
			- ```shell
			  yay -S baobab
			  ```
			- #### #Système/Paquets
				- [baobab](https://github.com/GNOME/baobab) : Utilitaire d'analyse de disque
			- #### Activation du trim
				- ```shell
				  sudo systemctl enable --now fstrim.timer
				  ```
	- ## #Réseau
	  collapsed:: true
		- ```shell
		  # NetworkManager
		  yay -S networkmanager network-manager-applet
		  
		  # Firewall
		  yay -S gufw
		  # yay -S firewalld
		  # sudo systemctl enable --now firewalld
		  ```
		- ### #Système/Paquets
		  collapsed:: true
			- [NetworkManager](https://gitlab.freedesktop.org/NetworkManager/NetworkManager) : #Système/OS/Processus/Daemon de gestion #Réseau développé en #C
			- [ufw](https://launchpad.net/ufw)
		- ### #Réseau/DNS
		  collapsed:: true
			- #### #Réseau/DNS over #Sécurité/Chiffrement/TLS avec **systemd-resolved** et **NetworkManager**
				- Configurer **systemd-resolved** dans */etc/systemd/resolved.conf*
				  logseq.order-list-type:: number
					- ```vim
					  [Resolve]
					  DNS=45.90.28.0#<dns-domain>
					  DNS=2a07:a8c0::#<dns-domain>
					  DNS=45.90.30.0#<dns-domain>
					  DNS=2a07:a8c1::#<dns-domain>
					  DNSSEC=yes
					  DNSOverTLS=yes
					  ```
				- Configurer **NetworkManager** pour qu'il pousse ses infos vers **systemd-resolved**
				  logseq.order-list-type:: number
					- ```vim
					  [main]
					  dns=systemd-resolved
					  systemd-resolved=false
					  ```
				- Activer **systemd-resolved** et redémarrer **NetworkManager**
				  logseq.order-list-type:: number
					- ```shell
					  sudo systemctl enable --now systemd-resolved
					  sudo systemctl restart NetworkManager
					  ```
				- Vérifier que tout fonctionne
				  logseq.order-list-type:: number
					- ```shell
					  resolvectl status
					  ```
	- ## #Système/Sauvegarde
	  collapsed:: true
		- ```shell
		  yay -S timeshift
		  ```
	- ## #[[Système/GUI/DE]]
	  collapsed:: true
		- ### #Système/GUI/DE/KDE
		- ### #Système/GUI/DE/GNOME
		  collapsed:: true
			- ```shell
			  # Installation
			  sudo pacman -Syu wayland gnome gdm gnome-power-manager
			  
			  # Activation du DM GNOME
			  sudo systemctl enable --now gdm.service
			  ```
		- ### #Système/GUI/DE/XFCE
	- ## #[[Système/GUI/WM]]
	  collapsed:: true
		- ```shell
		  # Hyprland
		  yay -S hyprland-git xdg-desktop-portal-hyprland-git
		  
		  # Verrouillage de session
		  yay -S hypridle-git hyprlock-git wlogout
		  
		  # Lanceur d'applications
		  yay -S rofi-lbonn-wayland-git
		  
		  # Barre de tâches
		  yay -S waybar-git
		  
		  # Gestionnaire de fonds d'écran
		  yay -S swww
		  
		  # Notifications
		  yay -S dunst
		  
		  # Captures d'écran
		  yay -S grimblast-git slurp swappy wf-recorder
		  
		  # Presse papier
		  yay -S cliphist
		  
		  # Gestionnaire de tâches
		  yay -S mission-center # GTK / windows like
		  yay -S btop # TUI
		  ```
		- ### Configuration Générale
		  collapsed:: true
			- Setup pour l'**association de fichiers** via explorateur (dolphin ou autre)
			  ```shell
			  sudo pacman -Syu archlinux-xdg-menu
			  xdg-menu
			  ```
			- Ajouter variable d'environnement 
			  ```
			  XDG_MENU_PREFIX=arch-
			  ```
			- Finaliser 
			  ```shell
			  reboot
			  kbuildsycoca6
			  ```
		- ### #Système/Paquets
			- #### WM
			  collapsed:: true
				- [Hyprland](https://github.com/hyprwm/Hyprland) : **Dynamic tiling Window Manager** développé en #Programmation/Langage/C++
					- [wiki](https://wiki.hyprland.org/)
			- #### Presse-papier
			  collapsed:: true
				- [cliphist](https://github.com/sentriz/cliphist) : gestionnaire léger développé en #Programmation/Langage/Go et interfaçable avec rofi
			- #### Notifications
			  collapsed:: true
				- [dunst](https://github.com/dunst-project/dunst) : daemon très léger développé en #C
			- #### Capture d'écran
			  collapsed:: true
				- [grimblast-git](https://github.com/hyprwm/contrib) : script #Système/Terminal/Shell pour prendre des **screenshots**
				- [slurp](https://github.com/emersion/slurp) : utilitaire pour **sélectionner des régions** de l'écran développé en #C
				  id:: 660e7aa6-a5eb-47b9-a13f-ae6502f98cfb
				- [swappy](https://github.com/jtheoof/swappy) : **éditeur de captures** d'écran développé en #C
				- [wf-recorder](https://github.com/ammen99/wf-recorder) : utilitaire développé en #Programmation/Langage/C++ pour **enregistrer l'écran** ou des **régions de l'écran** en combinaison avec [slurp](((660e7aa6-a5eb-47b9-a13f-ae6502f98cfb)))
				  ```shell
				  wf-recorder -g "$(slurp)"
				  ```
			- #### Lancement d'applications
			  collapsed:: true
				- [rofi](https://github.com/lbonn/rofi) : **lanceur d'applications** développé en #C très **personnalisable** et **léger**
			- #### Verrouillage de session
			  collapsed:: true
				- [hypridle](https://github.com/hyprwm/hypridle) : daemon d'**inactivité** pour **hyprland** développé en #Programmation/Langage/C++
				- [hyprlock](https://github.com/hyprwm/hyprlock) : ==alternative== à [swaylock](swaylock-effects-git) de l'environnement **Hypr** développé en #Programmation/Langage/C++
				- [swaylock-effects-git](https://github.com/mortie/swaylock-effects) : écran de **verrouillage** de session  **simple** et **personnalisable** développé en #C
				- [wlogout](https://github.com/ArtsyMacaw/wlogout) : menu de **verrouillage de session** développé en #C
			- #### Gestionnaire de fond d'écran
			  collapsed:: true
				- [swww](https://github.com/LGFae/swww) : daemon pour les **fonds d'écran** développé en #Programmation/Langage/Rust
			- #### Barre de tâches
			  collapsed:: true
				- [waybar](https://github.com/Alexays/Waybar) : barre de tâches très personnalisable dévelopée en #Programmation/Langage/C++
			- #### Gestionnaire de tâches
			  collapsed:: true
				- [MissionCenter](https://gitlab.com/mission-center-devs/mission-center) : Gestionnaire de tâches écrit en #Programmation/Langage/Rust
	- ## #[[Système/GUI/FM]]
	  collapsed:: true
		- ```shell
		  # Dolphin
		  yay -S dolphin ark kde-cli-tools
		  
		  # Nemo
		  yay -S nemo nemo-preview nemo-python nemo-fileroller nemo-audio-tab nemo-image-converter
		  
		  # Thunar
		  yay -S thunar thunar-archive-plugin
		  ```
		- ### #Système/Paquets
			- [dolphin](https://github.com/KDE/dolphin) : Gestionnaire de fichiers habituellement empaqueté avec #Système/GUI/DE/KDE #Programmation/Langage/C++
			  collapsed:: true
				- Interface configurable et bon panel de fonctionnalités.
				- Relativement plus "*lourd*" que d'autres options comme thunar. En particulier sur certaines machines **limitées en ressources**
			- [thunar](https://github.com/xfce-mirror/thunar) : Gestionnaire de fichiers habituellement empaqueté avec #Système/GUI/DE/XFCE et #Système/GUI/DE/GNOME #C
			  collapsed:: true
				- Facilement **configurable** et **léger** mais peut manquer de certaines fonctionnalités des explorateurs plus modernes
			- [nemo](https://github.com/linuxmint/nemo) : Gestionnaire de fichiers associé à #[[Système/OS/Desktop/Linux/Distro/Debian/Linux Mint]] et développé en #Programmation/Langage/C
			  collapsed:: true
				- ```apl
				  # A ajouter au début de /usr/bin/nemo-preview pour wayland
				  export GDK_BACKEND=x11
				  
				  # Configuration du terminal par défaut
				  exec = gsettings set org.cinnamon.desktop.default-applications.terminal exec kitty
				  ```
	- ## #Système/Terminal
	  collapsed:: true
		- ```shell
		  # Kitty
		  yay -S kitty
		  
		  # Alacritty
		  yay -S alacritty
		  ```
		- ### #Système/Paquets
			- [kitty](https://github.com/kovidgoyal/kitty) : #C #Programmation/Langage/Python
			- [alacritty](https://github.com/alacritty/alacritty) : #Programmation/Langage/Rust
	- ## #[[Système/GUI/DM]]
	  collapsed:: true
		- ```shell
		  # SDDM
		  yay -S sddm sddm-sugar-candy-git sddm-theme-corners
		  sudo systemctl enable --now sddm
		  
		  # Accès au répertoire utilisateur
		  setfacl -m u:sddm:x /home/username
		  setfacl -m u:sddm:r /home/username/.face.icon
		  ```
		- ### #Système/Paquets
			- [sddm](https://github.com/sddm/sddm) : #Programmation/Langage/C++
	- ## #Polkit
	  collapsed:: true
		- ```shell
		  # KDE
		  yay -S polkit-kde-agent
		  
		  # GNOME
		  yay -S polkit-gnome
		  ```
	- ## #Multimédia
	  collapsed:: true
		- ```shell
		  # Base
		  yay -S pipewire pipewire-jack pipewire-pulse pipewire-alsa wireplumber lib32-pipewire alsa-utils alsa-plugins alsa-firmware alsa-ucm-conf sof-firmware
		  
		  # Image / Vidéo
		  yay -S mpv-git imv-git imagemagick ffmpeg upscayl-bin
		  # yay -S vlc-git
		  
		  # Musique
		  yay -S audacious-git moc-pulse cava clyrics
		  
		  # Utilitaire
		  yay -S easyeffects-git easytag
		  ```
		- ### #Système/Paquets
			- [mpv](https://github.com/mpv-player/mpv) : lecteur **simple** et **léger** développé en #C
			  id:: 65e339f6-bfa5-451c-abdf-3581d36c6711
			- [imv](https://github.com/eXeC64/imv) : **visionneur d'images simple** et **léger** développé en #C
			- [audacious](https://github.com/audacious-media-player/audacious) : **lecteur** / **bibliothèque musicale** léger développé en #Programmation/Langage/C++
			- [MOC](https://moc.daper.net/) : **lecteur en mode console** léger développé en #C
			- [cava](https://github.com/karlstav/cava) : visualiseur audio développé en #C
			- [vlc](https://code.videolan.org/videolan/vlc) : lecteur **complet** mais parfois trop fourni / lourd en fonction de l'usage. Comporte quelques **problèmes d'implémentation Wayland**. Développé en #C et #Programmation/Langage/C++
			  collapsed:: true
				- VLC peut être **requis** par [dolphin](```shell
				  yay -S dolphin ark kde-cli-tools
				  ```) via **phonon-qt6-vlc** pour la lecture intégrée de certains médias (vidéo / musique)
				  - Une alternative consiste à installer **phonon-qt6-mpv-git** qui repose sur [mpv](((65e339f6-bfa5-451c-abdf-3581d36c6711))) et permet donc d'éviter d'installer VLC si non souhaité
				  - [easyeffects](https://github.com/wwmm/easyeffects)
				  - ## #Communication
				  collapsed:: true
				  - ```shell
				  # Client Discord
				  yay -S webcord
				  ```
		- ### #Système/Paquets
		  collapsed:: true
			- [Webcord](https://github.com/SpacingBat3/WebCord) : Client Discord plus respectueux de la vie privée
	- ## #Multimédia/Jeux
	  collapsed:: true
		- ```shell
		  # Proton
		  yay -S protonup-qt protontricks-git winetricks
		  
		  # Steam
		  yay -S steam steam-native-runtime steamtinkerlaunch
		  
		  # Other game launchers
		  yay -S heroic-games-launcher lutris
		  ```
		- ### #Système/Paquets
			- [protonup-qt](https://github.com/DavidoTek/ProtonUp-Qt)
	- ## #Système/Personnalisation
	  collapsed:: true
		- ### #Système/Paquets
			- ```shell
			  # QT
			  yay -S qt5ct qt6ct kvantum
			  
			  # GTK
			  yay -S nwg-look
			  nwg-look
			  ```
	- ## #Divers
	  collapsed:: true
		- ```shell
		  # Typing tests
		  yay -S toipe
		  ```
- # Maintenance
  collapsed:: true
	- ## Gestion des paquets
		- ### Mise à jour
		  collapsed:: true
			- #### Installation
			  collapsed:: true
				- Installe les mises à jour pour un ou plusieurs paquet ou tous les paquets si aucun n'est spécifié. Met également à jour l'index des paquets 
				  ```shell
				  sudo pacman -Syu <paquet>
				  ```
			- #### Suppression
			  collapsed:: true
				- **Suppression** d'un paquet et ses **dépendances orphelines** sans conserver de fichier *pacsave* sur le système 
				  ```shell
				  pacman -Rns <paquet>
				  ```
			- #### Orphelins
			  collapsed:: true
				- **Vérification** de la liste des paquets orphelins sur le système 
				  ```shell
				  pacman -Qtdq
				  ```
				- **Suppression** les paquets orphelins 
				  ```shell
				  pacman -Qtdq | pacman -Rns -
				  ```
				- [pacdiff](https://man.archlinux.org/man/pacdiff.8) : affiche les fichiers *pacnew* présents sur le système
			- #### Raison d'Installation
			  collapsed:: true
				- ```shell
				  # Explicitement installé
				  pacman -D --asexplicit <paquet>
				  
				  # Comme dépendance
				  pacman -S --asdeps <paquet>
				  ```
		- ### Gestion du cache des paquets
		  collapsed:: true
			- [paccache](https://man.archlinux.org/man/paccache.8) : permet de gérer le cache des paquets installés via pacman.
			  collapsed:: true
				- Pour **nettoyer** les paquets en cache et ne garde que les **3 derniers** pour chaque paquet 
				  ```shell
				  paccache -r
				  ```
				- *Dry run*, affiche les candidats à la suppression si l'on souhaite garder les **2 dernières** version de chaque paquet en cache 
				  ```shell
				  paccache -dk2
				  ```
				- Ne garder que les **2 dernières** version de chaque paquet en cache 
				  ```shell
				  paccache -rk2
				  ```
				- Activer le nettoyage hebdomadaire du cache 
				  ```shell
				  sudo systemctl enable --now paccache.timer
				  ```
		- ### Rétrograder un paquet
		  collapsed:: true
			- Rétrograder la version d'un paquet spécifié 
			  ```shell
			  downgrade <options> <pkg>
			  ```
				- Nécessite le paquet [downgrade](https://github.com/archlinux-downgrade/downgrade) 
				  ```shell
				  yay -S downgrade
				  ```
				- [Rétrograder via pacman](https://wiki.archlinux.org/title/downgrading_packages) : pacman stocke le **cache** des paquets installés dans **/var/cache/pacman/pkg**
					- Pour rétrograder 
					  ```shell
					  pacman -U /var/cache/pacman/pkg/mon_pkg.tar.zst
					  ```
		- ### Gestion des paquets python
		  collapsed:: true
			- #### Installation
				- Sur Arch il est préférable d'installer et de gérer les paquets python **via pacman** 
				  ```shell
				  sudo pacman -S python-"package"
				  sudo pacman -S python2-"package"
				  ```
			- #### Recompilation
				- Lorsqu'une nouvelle version de python est publiée sur les repos Arch, il faut **recompiler** tous les **paquets python issus du AUR** (les paquets des repos officiels sont gérés automatiquement)
				- Pour lister les paquets python à recompiler
				  ```shell
				  pacman -Qoq /usr/lib/python<ancienne_version>
				  ```
				- Pour les recompiler 
				  ```shell
				  yay -S $(pacman -Qoq /usr/lib/python3.11) --answerclean All
				  ```
	- ## Résolution de problèmes
		- ### Créer un fichier patch
		  collapsed:: true
			- Pour obtenir les différences entre des fichiers / dossiers
			- ```shell
			  diff -Naru file_original file_updated > file.patch # Un seul fichier
			  diff -crB dir_original dir_updated > dir.patch # Dossier
			  ```
			- `-N` : Traiter les fichiers absents comme des fichiers vides
			- `-a` : Traiter tous les fichiers comme des textes
			- `-r` : Comparer récursivement les sous-répertoires trouvés
			- `-u` : Afficher N (3 par défaut) lignes dans le context unifié
		- ### Compilation depuis un chroot propre
		  collapsed:: true
			- Utile si une mise à jour est bloquée à cause d'une **cassure de dépendance** ou autre
			- Quelques outils nécessaires 
			  logseq.order-list-type:: number
			  ```shell
			  yay -S devtools
			  ```
			- Créer un dossier vide qui accueillera l'environnement **propre**. Peut être créé **n'importe où** 
			  logseq.order-list-type:: number
			  ```shell
			  mkdir ~/Documents/chroot
			  ```
			- Définir une variable correspondant au dossier chroot pour faire plus simple 
			  logseq.order-list-type:: number
			  ```shell
			  CHROOT=$HOME/Documents/chroot
			  ```
			  Pour **fish** 
			  ```shell
			  set CHROOT $HOME/Documents/chroot
			  ```
			- Construire l'environnement **chroot** avec les bases nécessaires 
			  logseq.order-list-type:: number
			  ```shell
			  mkarchroot $CHROOT/root base-devel
			  ```
			- Mettre à jour le chroot si nécessaire 
			  logseq.order-list-type:: number
			  ```shell
			  arch-nspawn $CHROOT/root pacman -Syu
			  ```
			- Construire le paquet souhaité avec l'environnement propre
			  logseq.order-list-type:: number
			  id:: 65eb3f86-85fb-4f3e-b590-36d5f6b800e9
			  ```shell
			  makechrootpkg -c -r $CHROOT
			  ```
			  ==Il faut être dans le répertoire du paquet souhaité, là où se situe le fichier **PKGBUILD**==
			- Une fois le paquet construit, une archive est créée dan le répertoire de celui-ci. Il suffit de l'installer avec pacman 
			  logseq.order-list-type:: number
			  ```shell
			  sudo pacman -U <archive_du_paquet>
			  ```
			- Mettre à jour le système 
			  logseq.order-list-type:: number
			  ```shell
			  sudo pacman -Syu
			  ```
		- ### Erreurs #Sécurité/Chiffrement/GPG
		  collapsed:: true
			- Dan le cas d'une [Erreur ioctl](https://wiki.archlinux.org/title/GnuPG#Invalid_IPC_response_and_Inappropriate_ioctl_for_device)
				- Définir la variable d'environnement suivante pour que si besoin, #Sécurité/Chiffrement/GPG puisse utiliser le tty comme entrée
				  logseq.order-list-type:: number
				  ```shell
				  export GPG_TTY=$(tty)
				  ```
				- Editer le fichier ~/.gnupg/gpg-agent.conf pour définir la #Système/GUI à utiliser comme entrée ([pinentry](https://wiki.archlinux.org/title/GnuPG#pinentry))
				  logseq.order-list-type:: number
				  ```shell
				  echo "pinentry-program /usr/bin/pinentry-gtk" > ~/.gnupg/gpg-agent.conf
				  gpg-connect-agent reloadagent /bye
				  ```