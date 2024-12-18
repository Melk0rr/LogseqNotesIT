# #Sécurité/Chiffrement
collapsed:: true
	- [VeraCrypt](https://veracrypt.fr/en/Home.html) : Logiciel de chiffrement de données #OpenSource disponible sur #Système/OS/Desktop/Windows #Système/OS/Desktop/Linux et #Système/OS/Desktop/MACOS. Permet de créer des disques virtuels chiffrés ou tout simplement de chiffrer une partition ou un disque complet
- # #[[Sécurité/Offensif]]
  collapsed:: true
	- [HackTricks](https://book.hacktricks.xyz/welcome/readme) : encyclopédie en ligne sur des exploits et divers outils de #Sécurité/Offensif/Pentest
	- ## #Sécurité/Offensif/Obfuscation
		- [Anubis](https://github.com/0sir1ss/Anubis) : obscurcissement de code
	- ## #[[Réseau/Web/Site web]]
		- [XSStrike](https://github.com/s0md3v/XSStrike) : Détection de faille XSS
	- ## #Système/Logs
		- [Phant0m](https://github.com/olafhartong/Invoke-Phant0m/tree/master) : #OpenSource Script #Programmation/Langage/Powershell qui neutralise les processus de génération de logs sur Windows
	- ## #Sécurité/Offensif/Pentest/Bruteforce
		- [Hydra](https://github.com/vanhauser-thc/thc-hydra) : Programme #C de brute force de mots de passe
	- ## #[[Système/Administration/Active Directory]]
		- [gpp-decrypt](https://github.com/t0thkr1s/gpp-decrypt) : décrypte les cpasswords et mots de passe en clair dans les GPO
- # #[[Sécurité/Défensif]]
  collapsed:: true
	- [BlueTeam-Tools](https://github.com/A-poc/BlueTeam-Tools) : Repo github qui ressence divers outils de défense utiles
	- [grep.app](https://grep.app/) : Recherche de repository GIT
	- [WaybackMachine](https://archive.org/web/) : Archive Web
	- [Interact.sh](https://app.interactsh.com/#/) : Testeur de requêtes en ligne
	- ## #[[Système/Administration/Active Directory]]
		- [ADRecon](https://github.com/sense-of-security/ADRecon) : script #Programmation/Langage/Powershell d'extraction de données AD
		- [GPOZaurr](https://github.com/EvotecIT/GPOZaurr) : module #Programmation/Langage/Powershell qui permet de regrouper des données sur les GPO, générer des rapports et corriger des non conformités
	- ## #Analyse
		- [DeHashed](https://www.dehashed.com) : Base de données de HASH connus
		- [Hybrid Analysis](https://www.hybrid-analysis.com/) : Outil de sandbox en ligne
		- [MXToolBox](https://mxtoolbox.com) : Divers outils d'analyse
		- [VirusTotal](https://github.com/ventoy/Ventoy) : Analyse antivirus / IOC en ligne
	- ## #Réseau/DNS
		- [Anubis](https://github.com/jonluca/Anubis) : sondage et reconnaissance DNS
		- [CRT.sh](https://crt.sh/) : Scan de domain, d'URL / Ip,  whois
		- [DNSDumper](https://dnsdumpster.com/) : reconnaissance DNS
		- [FullHunt](https://fullhunt.io/) : Scan de domain
		- [ONYPHE](https://www.onyphe.io/) : Scan de domain
	- ## #Sécurité/Défensif/Forensic
		- [DFIR ORC](https://github.com/DFIR-ORC/dfir-orc) : Programme #Programmation/Langage/C++#OpenSource de collecte d'artefacts et IOC pour systèmes #Système/OS/Desktop/Windows
		- [Cyberchef](https://gchq.github.io/CyberChef) : Convertion et décryptage de formats de données variés
		- [Chainsaw](https://github.com/WithSecureLabs/chainsaw) : Programme #Programmation/Langage/Rust d'analyse d'artéfacts #Système/OS/Desktop/Windows
	- ## #Réseau/Communication/Mail
		- #Réseau/Communication/Mail/DMARC
			- [DMARCly](https://dmarcly.com/tools/) : Divers outils de vérification DMARC, DKIM et SPF
		- [Hunter](https://hunter.io/) : Recherche d'adresses mail liées à un site web
	- ## #Réseau
		- [malicious ip](https://github.com/romainmarcoux/malicious-ip/) : inventaire d'adresses IP malveillantes de type **scanners et bruteforce** => à bloquer en entrée (WAN -> LAN)
		- [malicious outgoing ip](https://github.com/ro mainmarcoux/malicious-outgoing-ip/tree/main) : inventaire d'adresses IP malveillantes de type **phishing, malware et C2** => à bloquer en sortie (LAN -> WAN)
	- ## #[[Réseau/Web/Site web]]
		- [exploit-db](https://www.exploit-db.com) : Recheche de vulnérabilités
		- [FOFA](https://en.fofa.info) : Propriétés d'un site web
		- [GrayhatWarfare](https://buckets.grayhatwarfare.com) : Propriétés d'un site web
		- [LeakIX](https://leakix.net) : Moteur de recherche Ips, Domains, filenames, hashes, ASN…
		- [Mitre](https://cve.mitre.org) : Recheche de vulnérabilités
		- [NetLas](https://app.netlas.io/) : Scan d'URL / Ip,  whois
		- [PulseDive](https://pulsedive.com) : Propriétés d'un site web
		- [SecurityTrails](https://securitytrails.com) : Moteur de recherche IP, mots clés, Hostname
		- [Shodan](https://www.shodan.io/) : Analyse et scan
		- [URLScan](https://urlscan.io/) : Analyse et scan
		- [Vulners](https://vulners.com) : Recheche de vulnérabilités
		- [ZoomEye](https://www.zoomeye.org) : Moteur de recherche de Vuln sur un site
	- ## #Système/OS/Desktop/Windows
		- [PatchaPalooza](https://github.com/xaitax/PatchaPalooza) : script #Programmation/Langage/Python de remontée des vulnérabilités récentes dans les produits Microsoft
		- [ScriptSentry](https://github.com/techspence/ScriptSentry) : script #Programmation/Langage/Powershell de découverte de scripts de connexion dangereux ou mal configurés
		- [DeepBlueCLI](https://github.com/sans-blue-team/DeepBlueCLI) : script #Programmation/Langage/Powershell d'analyse de #Système/Logs Windows Events
- # #[[Sécurité/Mots de passe]]
  collapsed:: true
	- [Bitwarden](https://bitwarden.com/) : #[[OpenSource]] Mots de passe stockés dans le cloud, synchronisation auto
	- [KeepassXC](https://keepassxc.org/) : #[[OpenSource]] Mots de passe chiffrés et stockés localement
	- [Lesspass](https://www.lesspass.com/#/) : #[[OpenSource]] Repose sur de la génération fonctionnelle, le mot de passe est calculé en fonction des paramètres donnés (mot de passe maître, site web, etc)
	- [Aegis](https://getaegis.app/) : #[[OpenSource]] Application 2FA avec import depuis Google Authenticator, 2FAS, LastPass, etc