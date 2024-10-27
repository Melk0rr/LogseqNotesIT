# #[[Gestion des droits]]
collapsed:: true
	- [Get-Acl](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-acl?view=powershell-7.3) **<option> <fichier / répertoire>** : Retourne la description de sécurité pour un fichier ou répertoire
- # #[[Sécurité/Mots de passe]]
  collapsed:: true
	- [ConvertFrom-SecureString](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/convertfrom-securestring?view=powershell-7.3) **<chaîne> <options>** : convertit une chaîne sécurisée en chaîne chiffrée standard
		- `"P@ssword1" | ConvertTo-SecureString -AsPlainText | ConvertFrom-SecureString | Out-File "C:\Temp\password"`
	- [ConvertTo-SecureString](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/convertto-securestring?view=powershell-7.3) **<chaîne> <options>** : convertit une chaîne de caractères en chaîne sécurisée
		- `"P@ssword1" | ConvertTo-SecureString -AsPlainText`
		- `Get-Content "C:\Temp\password" | ConvertTo-SecureString`