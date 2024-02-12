# Description
	- Distribution #Linux en #Rolling release et maintenue par la **communauté**
- # Installation
  id:: 65c8ff54-d1f3-41db-9746-5d11eec23b84
	- [Guide officiel](https://wiki.archlinux.org/title/Installation_guide_(Fran%C3%A7ais))
	  id:: 65c93b3e-72e6-4c5a-94e6-6528aba7488e
	- ## Base
		- ### Disposition clavier
		  collapsed:: true
			- `loadkeys fr` : change la configuration du clavier. Utile surtout pour les claviers non QWERTY
			  logseq.order-list-type:: number
		- ### Connexion à internet
		  collapsed:: true
			- `ping archlinux.org` : vérifie la connectivité internet. Mieux vaut une connexion ethernet pour se faciliter la vie
			  logseq.order-list-type:: number
		- ### Check UEFI
			- `ls /sys/firmware/efi/efivars` : s'assurer que l'installation est bien en mode **UEFI** (sauf si BIOS souhaité)
		- ### Horloge
			- `timedatectl` : pour vérifier que la date est bien valide
			  logseq.order-list-type:: number
		- ### Partitionnement
			- `lsblk` : affiche les disques et partitions actuelles (*blocs*) -> identifier le disque sur lequel installer le système
			  logseq.order-list-type:: number
			- `cfdisk <disque>` : exécute l'utilitaire [cfdisk](https://www.geeksforgeeks.org/cfdisk-command-in-linux-with-examples/) pour créer des partitions sur le disque sélectionné (e.g. nvme0n1)
			  logseq.order-list-type:: number
				- Dans la plupart des cas on veut une table de #Partitions **GPT**
				  logseq.order-list-type:: number
				- Si cfdisk ne demande pas le type souhaité -> s'assurer que le label *gpt* est présent
				  logseq.order-list-type:: number
				- Sinon ajouter le label manuellement avec [fdisk](https://www.geeksforgeeks.org/fdisk-command-in-linux-with-examples/)
				  logseq.order-list-type:: number
				- Partitionner le disque (c.f. ((65c8ff54-db3b-48de-b9d4-ece65f422173)))
				  logseq.order-list-type:: number
				- Quitter une fois les changements écrits
				  logseq.order-list-type:: number
		- ### Formatage
			- Pour l'exemple : <disque><partition x> => *nvme0n1px*
			- `lsblk` : pour vérifier les changements
			  logseq.order-list-type:: number
			- `mkfs.fat -F 32 <disque><partition efi>` (*nvme0n1p1*) : formate la partition **efi** en **FAT32** (pour la compatibilité)
			  logseq.order-list-type:: number
			- `mkswap <disque><partition swap>` (*nvme0n1p2*) : formate la partition **swap**, pas de formatage à proprement parlé`
			  logseq.order-list-type:: number
			- `swapon <disque><partition swap>` (*nvme0n1p2*) : active la partition **swap**
			  logseq.order-list-type:: number
			- `mkfs.ext4 <disque><partition racine>` (*nvme0n1p3*) : formate la partition **racine (/)** en **EXT4** (ou **BTRFS**, **NFS**, etc)
			  logseq.order-list-type:: number
			- `mkfs.ext4 <disque><partition home>` (*nvme0n1p4*) : idem pour la partition home
			  logseq.order-list-type:: number
		- ### Montage des partitions
			- `mount <disque><partition racine> /mnt` (*nvme0n1p3*) : **monte** la partition **racine** sur **/mnt**
			  logseq.order-list-type:: number
			- `mkdir /mnt/{efi,home}` : crée les répertoires **boot** et **home** qui serviront à monter nos autres partitions
			  logseq.order-list-type:: number
			- `mkdir /mnt/efi` : crée un répertoire **efi** si en mode **UEFI** (possible de monter sur /boot)
			  logseq.order-list-type:: number
			- `mount <disque><partition efi> /mnt/boot/efi` (*nvme0n1p1*) : **monte** la partition **efi** sur **/mnt/boot/efi**
			  logseq.order-list-type:: number
			- `mount <disque><partition home> /mnt/home` (*nvme0n1p4*) : **monte** la partition **home** sur **/mnt/home**
			  logseq.order-list-type:: number
	- ## Installation
		- ### Mirroirs`
			- reflector --country France --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist` : sélectionne les meilleurs miroirs
			  logseq.order-list-type:: number
			- `vim /etc/pacman.conf` : dé-commenter la section **multilib**
			  logseq.order-list-type:: number
		- ### Installation des paquets essentiels
			- `pacstrap /mnt base base-devel linux linux-firmware pacman-contrib nano networkmanager` : installe le système et quelques paquets essentiels
			  logseq.order-list-type:: number
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
			- `pacstrap /mnt efibootmgr os-prober` : installe des paquets relatifs au **boot**
			  logseq.order-list-type:: number
			- `pacstrap /mnt ntfs-3g exfat-utils mtools dosfstools` : paquets de manipulation de divers **systèmes de fichiers**
			  logseq.order-list-type:: number
			- `pacstrap /mnt man-db man-pages` : installe les pages de **manuels**
			  logseq.order-list-type:: number
			- Installer les paquets pour la gestion du **son**
			  logseq.order-list-type:: number
				- logseq.order-list-type:: number
				  ```
				  pacstrap /mnt pipewire pipewire-jack pipewire-pulse pipewire-alsa wireplumber lib32-pipewire alsa-utils alsa-plugins alsa-firmware alsa-ucm-conf sof-firmware
				  ```
		- ### Configuration système
			- `genfstab -U /mnt >> /mnt/etc/fstab` : génère le fichier fstab -> indique les **points de montage**
			  logseq.order-list-type:: number
			- `arch-chroot /mnt` : bascule sur le point de montage **racine**
			  logseq.order-list-type:: number
			- `nano /etc/hostname` : pour définir le **nom de la machine** sur le réseau
			  logseq.order-list-type:: number
			- `nano /etc/hosts` : pour définir la table locale
			  logseq.order-list-type:: number
				- ```
				  127.0.0.1  localhost
				  ::1  localhost
				  127.0.0.1  <hostname>.localdomain <hostname>
				  ```
			- `nano /etc/vconsole.conf` : pour définir la **disposition clavier** et la **police**
			  logseq.order-list-type:: number
				- `KEYMAP=fr-latin9`
				  logseq.order-list-type:: number
				- `FONT=eurlatgr`
				  logseq.order-list-type:: number
			- `nano /etc/locale.conf` : pour y définir les **locales**
			  logseq.order-list-type:: number
			- `nano /etc/locale.gen` : **dé-commenter** les langues souhaitées
			  logseq.order-list-type:: number
			- `locale-gen` : **génère les locales**
			  logseq.order-list-type:: number
			- `ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime` : crée un lien symbolique pour **définir le fuseau horaire**
			  logseq.order-list-type:: number
			- `hwclock --systohc` : ajuste l'**horloge**
			  logseq.order-list-type:: number
		- ### Installation chargeur d'amorçage
			- #### systemd-boot
				- `bootctl --path=/efi install` : installe systemd-boot
				  logseq.order-list-type:: number
					- Si l'installateur affiche une erreur concernant un problème de permissions
					  logseq.order-list-type:: number
						- `nano /etc/fstab` : s'assurer que la partition efi comporte `fmask=0137,dmask=0027`
						  logseq.order-list-type:: number
						- `umount /efi`
						  logseq.order-list-type:: number
						- `mount /efi`
						  logseq.order-list-type:: number
						- `bootctl update`
						  logseq.order-list-type:: number
			- `nano /efi/loader/loader.conf` : ajouter `default arch-*` pour définir une option par défaut (possible d'ajuster le **timeout** de démarrage). 
			  logseq.order-list-type:: number
			- `nano /efi/loader/entries/arch.conf` : ajouter les lignes sivantes
			  logseq.order-list-type:: number
				- ```
				  title   Arch Linux
				  linux   /vmlinuz-linux
				  initrd  /initramfs-linux.img
				  options root=/dev/nvme0n1p1 rw
				  ```
			- `systemctl enable NetworkManager` : active le gestionnaire réseau pour le redémarrage
			  logseq.order-list-type:: number
			- `exit` : pour revenir sur le **système temporaire**
			  logseq.order-list-type:: number
			- `umount -R /mnt` : démonter tout le contenu de **/mnt**
			  logseq.order-list-type:: number
			- `reboot`
			  logseq.order-list-type:: number