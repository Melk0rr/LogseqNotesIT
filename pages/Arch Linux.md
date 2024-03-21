# Description
	- Distribution #Linux en #Rolling release et maintenue par la **communauté**
- # Installation
  id:: 65c8ff54-d1f3-41db-9746-5d11eec23b84
	- [Guide officiel](https://wiki.archlinux.org/title/Installation_guide_(Fran%C3%A7ais))
	  id:: 65c93b3e-72e6-4c5a-94e6-6528aba7488e
	- ## Base
	  collapsed:: true
		- ### Disposition clavier
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
		- ### Check UEFI
			- S'assurer que l'installation est bien en mode **UEFI** (sauf si BIOS souhaité). Si la commande ne retourne rien: l'installation est en mode BIOS
			  ```shell
			  ls /sys/firmware/efi/efivars
			  ```
		- ### Horloge
			- Pour vérifier que la date est bien valide 
			  logseq.order-list-type:: number
			  ```shell
			  timedatectl
			  ```
		- ### Partitionnement
			- Afficher les disques et partitions actuelles (*blocs*) -> identifier le disque sur lequel installer le système 
			  logseq.order-list-type:: number
			  ```shell
			  lsblk
			  ```
			- Exécuter l'utilitaire [cfdisk](https://www.geeksforgeeks.org/cfdisk-command-in-linux-with-examples/) pour créer des partitions sur le disque sélectionné (e.g. nvme0n1) 
			  logseq.order-list-type:: number
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
		- ### Montage des partitions
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
		- ### Installation des paquets essentiels
			- Installer le système et quelques paquets essentiels 
			  logseq.order-list-type:: number
			  ```shell
			  pacstrap /mnt base base-devel linux linux-headers linux-firmware pacman-contrib nano networkmanager
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
			- Générer le fichier fstab -> indique les **points de montage** 
			  logseq.order-list-type:: number
			  ```shell
			  genfstab -U /mnt >> /mnt/etc/fstab
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
	- ## Post-installation
	  collapsed:: true
		- ### Base
			- ((65c92958-d6c2-4ea2-9cf7-d9d7ad35e33b)) + dé-commenter également les lignes suivantes
			  logseq.order-list-type:: number
			  ```
			  Color
			  VerbosePkgLists
			  ParallelDownloads = 5
			  ```
			- Créer un **nouvel utilisateur** (il faut éviter au maximum d'utiliser le **root**) et l'ajouter au groupe **wheel (sudoers)** 
			  logseq.order-list-type:: number
			  ```shell
			  useradd -m <utilisateur> -g wheel
			  ```
			- Définir un mot de passe pour le nouvel utilisateur 
			  logseq.order-list-type:: number
			  ```shell
			  passwd <utilisateur>
			  ```
			- Dé-commenter la ligne concernant le groupe **wheel** pour donner au groupe des **droits admins** 
			  logseq.order-list-type:: number
			  ```shell
			  vim /etc/sudoers
			  ```
		- ### AUR helper
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
		- ### #[[Firmware et support matériel]]
			- #### AMD
				- ```shell
				  sudo pacman -S --needed mesa-git lib32-mesa lib32-amdvlk vulkan-radeon vulkan-icd-loader lib32-vulkan-icd-loader
				  ```
	- ## Graphique
	  collapsed:: true
		- ### Général
			- #### Gestionnaire de fichiers
				- Installation de l'explorateur **dolphin**, gestionnaire de fichiers habituellement empaqueté avec **KDE**. Interface configurable et bon panel de fonctionnalités. Relativement plus "*lourd*" que d'autres options telles que thunar. En particulier sur certaines machines **limitées en ressources** 
				  ```shell
				  yay -S dolphin ark kde-cli-tools
				  ```
					- **ark** : utilitaire de gestion d'archives
					- **kde-cli-tools** : outils d'interaction système basé sur le framework **KDE**
				- Installation de l'explorateur **thunar**, gestionnaire de fichiers habituellement empaqueté avec **XFCE**. Facilement **configurable**, **léger** mais peut manquer de certaines fonctionnalités des explorateurs plus modernes 
				  ```shell
				  yay -S thunar thunar-archive-plugin
				  ```
			- #### Terminal
				- Installation d'Alacritty, émulateur de terminal développé en #Rust 
				  ```shell
				  yay -S alacritty
				  ```
				- Installation de Kitty, émulateur de terminal développé en #Python et #C 
				  ```shell
				  yay -S kitty
				  ```
			- #### Display Manger
				- Installation de **sddm**, écran de connexion personnalisable et habituellement empaqueté avec **KDE** 
				  ```shell
				  yay -S sddm sddm-sugar-candy-git sddm-theme-corners
				  ```
					- [sddm-sugar-candy-git](https://github.com/Kangie/sddm-sugar-candy)
					- [sddm-theme-corners-git](https://github.com/aczw/sddm-theme-corners)
				- Activation de sddm 
				  ```shell
				  sudo systemctl enable --now sddm
				  ```
			- #### Polkit
				- Installation du polkit KDE pour gérer le lancement d'applications graphiques nécessitant des droits admin 
				  ```shell
				  yay -S polkit-kde-agent
				  ```
			- #### Multimédia
				- Quelques lecteurs de médias 
				  ```shell
				  yay -S vlc-git mpv-git
				  ```
					- **vlc** : lecteur **complet** mais parfois trop fourni / lourd en fonction de l'usage. Comporte quelques **problèmes d'implémentation Wayland**
					- **mpv** : lecteur **simple** et **léger**
				- **Manipulation** / **conversion** d'images 
				  ```shell
				  yay -S imagemagick
				  ```
			- #### Personnalisation
				- Pour la configuration d'interfaces **QT5** et **QT6** 
				  ```shell
				  yay -S qt5ct qt6ct kvantum
				  ```
				- Pour la configuration d'interface **GTK3** 
				  ```shell
				  yay -S nwg-look
				  ```
		- ### Desktop Environment / Window Manager
		  collapsed:: true
			- #### Hyprland
				- Installation des paquets de base 
				  logseq.order-list-type:: number
				  ```shell
				  yay -S hyprland-git cliphist dunst grimblast-git rofi-lbonn-wayland-git slurp swaylock-effects-git swww waybar wlogout xdg-desktop-portal-hyprland
				  ```
					- **cliphist** : gestionnaire de presse-papier
					  logseq.order-list-type:: number
					- **dunst** : daemon de **notifications** très léger
					  logseq.order-list-type:: number
					- **grimblast-git** : pour prendre des **screenshots**
					  logseq.order-list-type:: number
					- **rofi-lbonn-wayland-git** : lanceur d'**applications**
					  logseq.order-list-type:: number
					- **slurp** : pour sélectionner des régions de l'écran
					  logseq.order-list-type:: number
					- **swaylock-effects-git** : utilitaire de **verrouillage** de session
					  logseq.order-list-type:: number
					- **swappy** : éditeur de captures d'écran
					  logseq.order-list-type:: number
					- **swww** : gestionnaire de **fonds d'écran**
					  logseq.order-list-type:: number
					- **waybar** : **barre** de tâches
					  logseq.order-list-type:: number
					- **wlogout** : gestionnaire de **verrouillage** / fermeture de session  / **mise en veille** / **arrêt** / **redémarrage**
					  logseq.order-list-type:: number
- # Maintenance
	- ## Gestion des paquets
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
	- ## Résolution de problèmes
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