
---

 Date de création : lundi 20 novembre 2023 08:41
 Matière : Software Security
 Enseignant : M. Roudier
 Tag :

---

![[04-SDLC-StaticAnalysis.pdf]]

---
## Secure SDLC

 Secure software development life cycle (Secure SDLC).
 
![[Pasted image 20231120084320.png]]

Lors d'un cycle de développement on a les tests classique mais on a également une phase d'analyse de risque et de test de pénétration.

Pour cela on a deux grandes approches :
- Sécurité par certification (approche après "sécurité après avoir codé")
	- Analyse statique et dynamique
	- Contrôle de flux d'information
	- Best practices, Security guidelines
- Sécurité par le design (approche "sécurité avant de coder")
	- Objectifs de sécurité
	- Analyse de menace


### Programmation défensive

#### Principe

Coder en s'assurant que certains grands principes soient respecté :
![[Pasted image 20231120084812.png]]

##### Secure the weakest link

Il faut penser aux attaques possibles.
Comment quelqu'un pourrait essayer d'attaquer ?
Qu'est-ce qu'il/elle pourrait vouloir accomplir/obtenir ?

Trouver le(s) lien(s) le(s) plus faible(s)
- La librairie de cryptographie est probablement très bien
- Est ce qu'il y a un moyen de contourner la cryptographie ?
	- La donnée est stockée de façon encrypté, où est ce que la clé est stockée ?

Pour faire simple il faut faire des analyses de sécurité sur tout le système et passer du temps là où c'est réellement important.

### Catégories générales 

![[Pasted image 20231120085144.png]]

### Tester un logiciel sécurisé

![[Pasted image 20231120085213.png]]

Pour cela on a deux possibilités :
- Analyse statique (on inspecte le code ou on lance une méthode automatisé pour trouver les erreurs ou gagner de la confiance à propose de leur absence).
	- Considère tous les inputs possible (de façon sommaire)
	- Trouve les bugs et les vulnérabilités
	- Peut prouver l'absence de bugs dans certains cas
- Analyse dynamique (On lance le code, supposément dans des conditions prédéfinies pour voir s'il y a des problèmes).
	- On doit choisir un échantillons d'input pour l'entrée
	- Permet de trouver les bugs et les vulnérabilités
	- Ne peut pas prouver leur absence

#### Analyse statique

![[Pasted image 20231120085557.png]]

### Reverse Engineering (for pentesting)

Une forme spéciale d'analyse statique
- Un utilisateur expérimenté est requis
- Le principe est d'étudier un programme pour voir son fonctionnement et trouver des vulnérabilités qui peuvent être exploité dans un logiciel closed source (opposé de open source)
- Cela peut permettre de trouver des backdoors (insider attack...)
- C'est aussi utilisé pour étudier des virus et de voir comment il exploite les logiciels/le système

On va transformer le binaire en :
- Code assembler (given file format) :
	- Executable et linkable format (ELF) - Linux
	- Portable Executable (PE) Format - Windows
	- Match-Object (Mach-O) - OSX et IOS
	- ART (replaçant de Dalvik) - Android
- Code source (Moins commun, par exemple Java désassemblé à partir du byte code)

Le revserse engineering va nécessiter un outil de désassemblage :
![[Pasted image 20231120090227.png]]

Il faudra aussi probablement un débugger et un assembler pour modifier le code assembleur :
![[Pasted image 20231120090258.png]]

![[Pasted image 20231120090310.png]]

![[Pasted image 20231120090317.png]]

![[Pasted image 20231120090326.png]]

![[Pasted image 20231120090332.png]]

![[Pasted image 20231120090340.png]]

![[Pasted image 20231120090350.png]]

![[Pasted image 20231120090402.png]]

![[Pasted image 20231120090410.png]]

![[Pasted image 20231120090416.png]]

![[Pasted image 20231120090421.png]]