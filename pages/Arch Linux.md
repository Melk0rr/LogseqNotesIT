# Description
collapsed:: true
	- Distribution #Linux créée en 2002 par Judd Vinet. Elle suit le principe **KISS**: Keep It Simple, Stupid
	- ## Caractéristiques
	  collapsed:: true
		- |**Modèle**|Communautaire|
		  |**Mise à jour**|Rolling release|
		  |**Public**|Expérimenté|
		  |**Usage**|Personnel|
		  |**Famille**|Arch Linux|
		  |**Basé sur**|Indépendant|
		  |**Base de**|BlackArch, EndeavourOS, Manjaro, CachyOS|
		  |**Gestionnaire de paquets**|pacman|
		  |**Format de paquet**|#PKG [:br]TAR.ZST|
		  |**Installateur graphique**|NON|
		  |**Approche infra**|Traditionnelle|
		  |**Site web**|[archlinux.org](http://archlinux.org)|
- # Installation
  id:: 65c8ff54-d1f3-41db-9746-5d11eec23b84
  collapsed:: true
	- [Guide officiel](https://wiki.archlinux.org/title/Installation_guide_(Fran%C3%A7ais))
	  id:: 65c93b3e-72e6-4c5a-94e6-6528aba7488e
	- ## Base
	  collapsed:: true
		- ### Disposition clavier
		  collapsed:: true
			- Changer la configuration du clavier. Utile surtout pour les claviers non QWERTY 
			  logseq.order-list-type:: number
			  ```shell
			  loadkeys fr
			  ```
		- ### Connexion à internet
		  collapsed:: true
			- Vérifier la connectivité internet. Mieux vaut une connexion ethernet pour se faciliter la vie 
			  logseq.order-list-type:: number
			  ```shell
			  ping archlinux.org
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
			  timedatectl
			  ```
		- ### Partitionnement
		  collapsed:: true
			- Afficher les disques et partitions actuelles (*blocs*) -> identifier le disque sur lequel installer le système 
			  logseq.order-list-type:: number
			  ```shell
			  lsblk
			  ```
			- Exécuter l'utilitaire [cfdisk](https://www.geeksforgeeks.org/cfdisk-command-in-linux-with-examples/) pour créer des partitions sur le disque sélectionné (e.g. nvme0n1) 
			  logseq.order-list-type:: number
			  collapsed:: true
			  ```shell
			  cfdisk <disque>
			  ```
				- Dans la plupart des cas on veut une table de #Partitions **GPT**
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
			  e2label /dev/XXX "new label" # ext2/3/4
			  btrfs filesystem label /dev/XXX "new label" # btrfs
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
		- ### Installation des #Paquets essentiels
		  collapsed:: true
			- Installer le système et quelques paquets essentiels 
			  logseq.order-list-type:: number
			  ```shell
			  pacstrap /mnt base base-devel linux linux-headers linux-firmware pacman-contrib nano networkmanager firewalld
			  ```
				- **base** : installation minimale d'Arch linux
				  logseq.order-list-type:: number
				- **linux** : noyau linux
				  logseq.order-list-type:: number
				- **linux-firmware** : firmware utiles pour certains composants matériel (clavier, souris, etc.)
				  logseq.order-list-type:: number
				- **pacman-conrib** : utilitaire pour le maintien de Arch
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
			- Ajouter les lignes sivantes 
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
			- Activer le gestionnaire réseau pour le redémarrage 
			  logseq.order-list-type:: number
			  ```shell
			  systemctl enable --now NetworkManager
			  ```
			- Installation des mises à jour **microcode** pour le processeur (AMD) 
			  logseq.order-list-type:: number
			  ```shell
			  pacman -S amd-ucode
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
	  collapsed:: true
		- ### #Mirroirs
		  collapsed:: true
			- ((65c92958-d6c2-4ea2-9cf7-d9d7ad35e33b)) + dé-commenter également les lignes suivantes
			  logseq.order-list-type:: number
			  ```
			  Color
			  VerbosePkgLists
			  ParallelDownloads = 5
			  ```
		- ### [Utilisateurs](((668d2260-0977-49ba-a543-1d5610274a5c)))
		- ### #[[AUR helper]]
		  collapsed:: true
			- #### [Yay](((654cd0e6-59fd-492f-9c7a-3300b72b7da2)))
				- logseq.order-list-type:: number
				  ```shell
				  sudo pacman -S --needed git base-devel
				  git clone https://aur.archlinux.org/yay-bin.git
				  cd yay-bin
				  makepkg -si
				  ```
				- Support mises à jour git 
				  logseq.order-list-type:: number
				  ```shell
				  yay -Y --gendb
				  yay -Y --devel --save
				  ```
			- #### [Paru](((657ac02b-fd09-4dbd-ac7b-862e422ee55a)))
- # Post-installation
  collapsed:: true
	- ## #[[Firmware et support matériel]]
	  collapsed:: true
		- ### #AMD
		  collapsed:: true
			- #### #Paquets
				- Installation par défaut (**mesa** ou **mesa-git**)
				  ```shell
				  sudo pacman -S --needed mesa-git lib32-mesa vulkan-radeon vulkan-icd-loader lib32-vulkan-icd-loader
				  ```
				- Installation [mesa-tkg](https://github.com/Frogging-Family/mesa-git) : version maintenue par **TKG** -> contient des patchs et fixes supplémentaires
				  ```shell
				  git clone https://github.com/Frogging-Family/mesa-git
				  cd mesa-tkg
				  makepkg -si
				  ```
				- ==Ne pas installer== **amdvlk** ou **lib32-amdvlk** : ces paquets s'imposent comme paquets par défaut et peuvent causer beaucoup de problèmes
			-
		- ### #Impression
		  collapsed:: true
			- #### Général
			  collapsed:: true
				- ##### #Paquets
					- ```shell
					  yay -S ghostscript gsfonts cups cups-filters cups-pdf system-config-printer avahi foomatic-db-engine foomatic-db foomatic-db-ppds foomatic-db-nonfree foomatic-db-nonfree-ppds gutenprint foomatic-db-gutenprint-ppds
					  ```
				- ##### #Daemon
				  collapsed:: true
					- ```shell
					  sudo systemctl enable --now avahi-daemon
					  sudo systemctl enable --now cups
					  ```
			- #### Epson
			  collapsed:: true
				- ##### #Paquets
				  collapsed:: true
					- ```shell
					  yay -S epson-inkjet-printer-escpr epson-inkjet-printer-escpr2
					  ```
			- #### HP
			  collapsed:: true
				- ##### #Paquets
					- ```shell
					  yay -S hplip
					  ```
		- ### #Bluetooth
		  collapsed:: true
			- #### #Paquets
			  collapsed:: true
				- ```shell
				  yay -S bluez bluez-plugins bluez-utils
				  ```
			- #### #Daemon
			  collapsed:: true
				- ```shell
				  sudo systemctl enable --now bluetooth
				  ```
	- ## #[[Desktop Environment]]
	  collapsed:: true
		- ### #KDE
		- ### #GNOME
		- ### #XFCE
	- ## #[[Window Manager]]
	  collapsed:: true
		- ### Général
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
		- ### #Hyprland
		  collapsed:: true
			- [Wiki Hyprland](https://wiki.hyprland.org/)
			- #### #Paquets de base
			  collapsed:: true
				- ```shell
				  yay -S hyprland-git xdg-desktop-portal-hyprland-git
				  ```
				- Recommandé d'utiliser la version **hyprland-git**
				  collapsed:: true
					- Les développeurs d'hyprland sont très **réactifs**
					- Les bugs sont **fix très rapidement**
					- Permet d'avoir les tous **derniers correctifs**
			- #### #Paquets de gestion de presse-papier
			  collapsed:: true
				- ```shell
				  yay -S cliphist
				  ```
				- [cliphist](https://github.com/sentriz/cliphist) : gestionnaire léger développé en #Go et interfaçable avec rofi
			- #### #Paquets d'affichage de notifications
			  collapsed:: true
				- ```shell
				  yay -S dunst
				  ```
				- [dunst](https://github.com/dunst-project/dunst) : daemon très léger développé en #C
			- #### #Paquets de capture d'écran
			  collapsed:: true
				- ```shell
				  yay -S grimblast-git slurp swappy wf-recorder
				  ```
				- [grimblast-git](https://github.com/hyprwm/contrib) : script #Shell pour prendre des **screenshots**
				- [slurp](https://github.com/emersion/slurp) : utilitaire pour **sélectionner des régions** de l'écran développé en #C
				  id:: 660e7aa6-a5eb-47b9-a13f-ae6502f98cfb
				- [swappy](https://github.com/jtheoof/swappy) : **éditeur de captures** d'écran développé en #C
				- [wf-recorder](https://github.com/ammen99/wf-recorder) : utilitaire développé en #C++ pour **enregistrer l'écran** ou des **régions de l'écran** en combinaison avec [slurp](((660e7aa6-a5eb-47b9-a13f-ae6502f98cfb)))
				  ```shell
				  wf-recorder -g "$(slurp)"
				  ```
			- #### #Paquets de lancement d'applications
			  collapsed:: true
				- ```shell
				  yay -S rofi-lbonn-wayland-git
				  ```
				- [rofi](https://github.com/lbonn/rofi) : **lanceur d'applications** développé en #C très **personnalisable** et **léger**
			- #### #Paquets pour verrouillage de session
			  collapsed:: true
				- ```shell
				  yay -S hypridle swaylock-effects-git wlogout
				  ```
				- [hypridle](https://github.com/hyprwm/hypridle) : daemon d'**inactivité** pour **hyprland** développé en #C++
				- [swaylock-effects-git](https://github.com/mortie/swaylock-effects) : écran de **verrouillage** de session  **simple** et **personnalisable** développé en #C
				- [hyprlock](https://github.com/hyprwm/hyprlock) : ==alternative== à [swaylock](swaylock-effects-git) de l'environnement **Hypr** développé en #C++
				- [wlogout](https://github.com/ArtsyMacaw/wlogout) : menu de **verrouillage de session** développé en #C
			- #### #Paquets de gestion de fond d'écran
			  collapsed:: true
				- ```shell
				  yay -S swww-git
				  ```
				- [swww](https://github.com/LGFae/swww) : daemon pour les **fonds d'écran** développé en #Rust
			- #### #Paquets de gestion barre de tâches
			  collapsed:: true
				- ```shell
				  yay -S waybar-git
				  ```
				- [waybar](https://github.com/Alexays/Waybar) : barre de tâches très personnalisable dévelopée en #C++
	- ## #[[Gestionnaire de fichiers]]
	  collapsed:: true
		- ### Dolphin
		  collapsed:: true
			- Gestionnaire de fichiers habituellement empaqueté avec #KDE.
			- Interface configurable et bon panel de fonctionnalités.
			- Relativement plus "*lourd*" que d'autres options comme thunar. En particulier sur certaines machines **limitées en ressources**
			- #### #Paquets
			  collapsed:: true
				- id:: 65cfcd67-02fa-424c-9c87-a8f347546160
				  collapsed:: true
				  ```shell
				  yay -S dolphin ark kde-cli-tools
				  ```
					- **ark** : utilitaire de gestion d'archives
					- **kde-cli-tools** : outils d'interaction système basé sur le framework **KDE**
		- ### Thunar
		  collapsed:: true
			- Gestionnaire de fichiers habituellement empaqueté avec #XFCE et #GNOME.
			- Facilement **configurable** et **léger** mais peut manquer de certaines fonctionnalités des explorateurs plus modernes
			- #### #Paquets
				- ```shell
				  yay -S thunar thunar-archive-plugin
				  ```
	- ## #Terminal
	  collapsed:: true
		- ### Alacritty
			- Emulateur de terminal développé en #Rust 
			  ```shell
			  yay -S alacritty
			  ```
		- ### Kitty
		  collapsed:: true
			- Emulateur de terminal développé en #Python et #C 
			  ```shell
			  yay -S kitty
			  ```
	- ## #[[Display Manger]]
	  collapsed:: true
		- ### SDDM
			- Ecran de connexion personnalisable. Habituellement empaqueté avec #KDE
			- #### #Paquets
			  collapsed:: true
				- collapsed:: true
				  ```shell
				  yay -S sddm sddm-sugar-candy-git sddm-theme-corners
				  ```
					- [sddm-sugar-candy-git](https://github.com/Kangie/sddm-sugar-candy)
					- [sddm-theme-corners-git](https://github.com/aczw/sddm-theme-corners)
			- #### Activation
			  collapsed:: true
				- ```shell
				  sudo systemctl enable --now sddm
				  ```
			- #### Accès au répertoire utilisateur
			  collapsed:: true
				- ```shell
				  setfacl -m u:sddm:x /home/username
				  setfacl -m u:sddm:r /home/username/.face.icon
				  ```
	- ## #Polkit
	  collapsed:: true
		- ### #KDE
		  collapsed:: true
			- #### #Paquets
			  collapsed:: true
				- ```shell
				  yay -S polkit-kde-agent
				  ```
		- ### #GNOME
		  collapsed:: true
			- #### #Paquets
			  collapsed:: true
				- ```shell
				  yay -S polkit-gnome
				  ```
	- ## #Multimédia
	  collapsed:: true
		- ### Lecture de médias
		  collapsed:: true
			- #### #Paquets
			  collapsed:: true
				- ```shell
				  yay -S mpv-git imv-git audacious-git
				  ```
				- [mpv](https://github.com/mpv-player/mpv) : lecteur **simple** et **léger** développé en #C
				  id:: 65e339f6-bfa5-451c-abdf-3581d36c6711
				- [imv](https://github.com/eXeC64/imv) : **visionneur d'images simple** et **léger** développé en #C
				- [audacious](https://github.com/audacious-media-player/audacious) : **lecteur** / **bibliothèque musicale** léger développé en #C++
				- [vlc](https://code.videolan.org/videolan/vlc) : lecteur **complet** mais parfois trop fourni / lourd en fonction de l'usage. Comporte quelques **problèmes d'implémentation Wayland**. Développé en #C et #C++
				  collapsed:: true
					- VLC peut être **requis** par [dolphin](((65cfcd67-02fa-424c-9c87-a8f347546160))) via **phonon-qt6-vlc** pour la lecture intégrée de certains médias (vidéo / musique)
					- Une alternative consiste à installer **phonon-qt6-mpv-git** qui repose sur [mpv](((65e339f6-bfa5-451c-abdf-3581d36c6711))) et permet donc d'éviter d'installer VLC si non souhaité
		- ### Manipulation / conversion d'images
		  collapsed:: true
			- #### #Paquets
			  collapsed:: true
				- ```shell
				  yay -S imagemagick ffmpeg
				  ```
	- ## #Jeux
	  collapsed:: true
		- ### #Paquets
		  collapsed:: true
			- ```shell
			  yay -S steam steam-native-runtime steamtinkerlaunch protonup-qt protontricks-git winetricks heroic-games-launcher lutris
			  ```
	- ## Personnalisation
	  collapsed:: true
		- ### Interfaces #QT
		  collapsed:: true
			- #### #Paquets
			  collapsed:: true
				- ```shell
				  yay -S qt5ct qt6ct kvantum
				  ```
		- ### Interfaces #GTK
		  collapsed:: true
			- #### #Paquets
			  collapsed:: true
				- ```shell
				  yay -S nwg-look
				  ```
- # Maintenance
  collapsed:: true
	- ## Gestion des paquets
	  collapsed:: true
		- ### Mise à jour
		  collapsed:: true
			- Installe les mises à jour pour un ou plusieurs paquet ou tous les paquets si aucun n'est spécifié. Met également à jour l'index des paquets 
			  ```shell
			  sudo pacman -Syu <paquet>
			  ```
			- **Suppression** d'un paquet et ses **dépendances orphelines** sans conserver de fichier *pacsave* sur le système 
			  ```shell
			  pacman -Rns <paquet>
			  ```
			- **Vérification** de la liste des paquets orphelins sur le système 
			  ```shell
			  pacman -Qtdq
			  ```
			- **Suppression** les paquets orphelins 
			  ```shell
			  pacman -Qtdq | pacman -Rns -
			  ```
			- [pacdiff](https://man.archlinux.org/man/pacdiff.8) : affiche les fichiers *pacnew* présents sur le système
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
	  collapsed:: true
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
		- ### Erreurs #GPG
		  collapsed:: true
			- Dan le cas d'une [Erreur ioctl](https://wiki.archlinux.org/title/GnuPG#Invalid_IPC_response_and_Inappropriate_ioctl_for_device)
				- Définir la variable d'environnement suivante pour que si besoin, #GPG puisse utiliser le tty comme entrée
				  logseq.order-list-type:: number
				  ```shell
				  export GPG_TTY=$(tty)
				  ```
				- Editer le fichier ~/.gnupg/gpg-agent.conf pour définir la #GUI à utiliser comme entrée ([pinentry](https://wiki.archlinux.org/title/GnuPG#pinentry))
				  logseq.order-list-type:: number
				  ```shell
				  echo "pinentry-program /usr/bin/pinentry-gtk" > ~/.gnupg/gpg-agent.conf
				  gpg-connect-agent reloadagent /bye
				  ```