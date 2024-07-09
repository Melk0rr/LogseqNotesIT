# Description
collapsed:: true
	- Famille d'#[[Operating System]] basée sur #Unix créée en 1991 par Linus Torvalds
- # #Distributions
  collapsed:: true
	- ![Linux distributions tree](./assets/Linux Distributions Timeline.svg)
	- ## #Debian
	- ## #openSUSE
	- ## #[[Arch Linux]]
- # Installation
	- ## #Partitions
	  id:: 65c8ff54-db3b-48de-b9d4-ece65f422173
	  collapsed:: true
		- [efi](https://wiki.archlinux.org/title/EFI_system_partition) : partition dédiée au **chargeur d'amorçage** (*boot loader*).
			- Minimum **1Go** requis dans la plupart des cas surtout si plusieurs kernels utilisés
		- [swap](https://wiki.archlinux.org/title/swap) : espace ou fichier utilisé pour **étendre la mémoire physique**. Pour faire simple, si toute la mémoire RAM est utilisée, alors le système utilisera l'espace swap en attendant que la RAM ne se libère. Les opérations utilisant le swap sont bien plus **lentes** que lorsque le système utilise la mémoire vive.
			- Une partition swap n'est plus vraiment requise dans la mesure où les quantités de RAM sont généralement élevées.
			- Une partition swap est requise si le système est configuré pour de l'==hibernation==
			  id:: 65c8ff54-14ef-48dd-8926-c07e0b1ca4f6
				- RAM **8Go**:  ~~hibernation~~ => **3Go** / *hibernation* => **11Go**
				- RAM **16Go** : ~~hibernation~~ => **4Go** / *hibernation* => **20Go**
				- RAM **32Go** : ~~hibernation~~ => **6Go** / *hibernation* => **38Go**
				- RAM **64Go** : ~~hibernation~~ => **8Go** / *hibernation* => **72Go**
		- [root (/)](https://wiki.archlinux.org/title/Partitioning#/) : partition racine qui accueille le système de fichiers
		- [home (/home)](https://wiki.archlinux.org/title/Partitioning#/) : répertoire contenant les fichiers utilisateurs