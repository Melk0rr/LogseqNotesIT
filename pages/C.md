# Description
collapsed:: true
	- Langage de #Programmation **impératif**, **compilé** et **bas niveau** inventé au début des années 1970
	-
- # Avantages & Inconvénients
  collapsed:: true
	- ## Avantages
		- Rapide
		- Gestion de la mémoire
		- Optimisation
	- ## Inconvénients
		- Gestion des chaines de caractères
		- Fuites mémoire
- # Notions
  collapsed:: true
	- ## #Types
	  id:: 66741c79-5e65-4f51-b3c6-00e62a28c6d0
	  collapsed:: true
		- | **Type** | **Mémoire (octets / arch)** | **Valeur(min)** | **Valeur(max)** |
		  | :---: | :---: | :---: | :---: |
		  | *char* | - | - | - |
		  | *signed char* | 1 | -128 | 127 |
		  | *unsigned char* | 1 | 0 | 255 |
		  | *int* | 2 / 4 | -32 768 / -2 147 483 648 | 32 767 / 2 147 483 647 |
		  | *unsigned int* | 2 / 4 | 0 / 0 | 65 535 / 4 294 967 295 |
		  | *short* | 2 | -32768 | 32 767 |
		  | *unsigned short* | 2 | 0 | 65 535 |
		  | *long* | 4 | -2 147 483 648 | 2 147 483 647 |
		  | *unsingned long* | 4 | 0 | 4 294 967 295 |
		  | *long long* | 8 | -9 223 372 036 854 780 000 | 9 223 372 036 854 780 000 |
		  | *unsigned long long* | 8 | 0 | 18 446 744 073 709 600 000 |
		  | *float* | 4 | -3.4e38 | 3.4e38 |
		  | *double* | 8 | -1.7e308 | 1.7e308 |
		  | *long double* | 10 | -1.1e4932 | 1.1e4932 |
	- ## #Variables
	  id:: 66740240-b7ba-4a5e-af69-4110f0d7b628
	  collapsed:: true
		- #### Utilisation
			- ```c
			  int maVariable = 3;	 // Déclaration et initialisation de la variable
			  
			  printf(maVariable);  // Valeur de la variable
			  printf(&maVariable); // Adresse de la variable
			  ```
	- ## #Pointeurs
	  id:: 6673ffb0-886e-4e73-a0fd-1cdabff8510a
	  collapsed:: true
		- Un pointeur est une variable qui contient l**'adresse** (et non la valeur) d'une autre variable
		- #### Utilisation
			- ```c
			  *monPointeur = NULL;		// Déclaration et initialisation du pointeur
			  *monPointeur = &maVariable; // Déclaration et initialisation du pointeur
			  
			  printf(monPointeur);		// Adresse de la variable pointée
			  printf(*monPointeur);		// Valeur de la variable pointée
			  printf(&monPointeur);		// Adresse du pointeur
			  ```
- # Usages
  collapsed:: true
	- Systèmes d'exploitation
	- Systèmes embarqués
	- Compilateurs
- # Influences
  collapsed:: true
	- Langage B
	- Fortran