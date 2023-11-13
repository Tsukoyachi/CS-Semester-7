---
dg-publish: "true"
---
---

 Date de création : lundi 13 novembre 2023 08:10
 Matière : Software Security
 Enseignant : M. Roudier
 Tag :

---

 ![[03-ArchiControleAccesv2.pdf]]

---

### Qu'est ce qu'un contrôle d'accès ?

 ![[Pasted image 20231113081119.png]]

En supposant :
- Que le système sait qui est l'utilisateur
	- Par exemple avec une authentification via nom et mot de passe, ou d'autres identifiants
- La requête d'accès passe par un gardien (Reference monitor)
	- Le système ne doit pas permettre se gardien d'être contourné

Un contrôle d'accès va permettre de filtrer les personnes ayant accès à tel ou tel ressources. Quand les deux suppositions précédentes sont remplies, alors un utilisateur autorisé pourra accéder à une ressource lorsqu'il fait une requête pour y accéder, et inversement si un utilisateur non autorisé veut accéder à une ressource il sera rejeté.

On peut modéliser cela via **une matrice de contrôle d'accès** :
![[Pasted image 20231113081606.png]]

### Rôles (aka Groupes)

Un rôle correspond à un ensemble d'utilisateur.
- Admnistrateur, Sur-utilisateur, Utilisateur, Invité,...

On peut assigner des permissions aux rôles, chaque utilisateur obtient des permissions.

En général on observe une hiérarchie des rôles :
- Un ordre partiel des rôles
- Chaque rôle possède également les permissions des rôles inférieurs.
- Chaque rôle ne va donc lister que les permissions des rôles inférieurs.

![[Pasted image 20231113081909.png]]

#### Contrôle d'accès par le rôle

![[Pasted image 20231113081938.png]]

Ce schéma résume bien le workflow d'un contrôle d'accès par rôle. Un ou plusieurs individus vont être associé à un rôle qui lui aura accès à des ressources. Donc par le biais du rôle les individus ont accès à divers ressources.

#### Concepts d'implémentation

![[Pasted image 20231113082135.png]]

On possède une list de contrôle d'accès ()