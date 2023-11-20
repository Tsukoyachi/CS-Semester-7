---
dg-publish: "true"
---
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
	- Considère tous les inputs possible (de faç)
- Analyse dynamique (On lance le code, supposément dans des conditions prédéfinies pour voir s'il y a des problèmes).

