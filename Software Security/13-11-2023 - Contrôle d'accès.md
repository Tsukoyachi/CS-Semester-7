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
- Administrateur, Sur-utilisateur, Utilisateur, Invité,...

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

Ici on voit deux concepts, celui d'implémentation par ACL et celui de capacité d'un utilisateur.

On possède une list de contrôle d'accès (ACL en anglais)
- Elle va permettre de stocker les colonnes de la matrice de contrôle d'accès avec les ressources.
![[Pasted image 20231113082135.png]]

Capacité :
- Un utilisateur aura un "ticket" pour chaque ressource
- 2 variantes
	- Stocker les lignes de la matrice avec l'utilisateur, sous contrôle de l'OS
	- Un ticket non modifiable (un ticket signé par exemple, cf [[23-10-2023 - Cryptographie]]) en espace utilisateur.

![[Pasted image 20231113083046.png]]

### Contrôle d'accès en résumé

Un contrôle d'accès utilise un gardien (reference monitor)
- Vérification des permissions : <info utilisateur, action> -> oui/non 
- Important : **Il ne doit pas y avoir de moyen de contourner cette vérification.**

Matrice de contrôle d'accès :
- ACL vs capacité
- Avantage et désavantages dans les deux cas.

Contrôle d'accès basé sur les rôles :
- Ici il faut utilisé le groupe/rôle à la places des "infos utilisateurs", peuvent utiliser une hiérarchie de groupe.

### Contrôle d'accès sous Linux

Un processus possède l'id utilisateur.
- Il l'obtient lors du processus de création.
	- Ensemble de permissions limités
	- Id spécial pour le rôle "root"
		- Toutes les permissions sont données
- Les fichiers ont une ACL
	- Donne des permissions à certains id utilisateur
	- Owner, Group, Other

Chaque fichier possède un utilisateur et un groupe. Les permissions sont données par l'owner.
- Lire, écrire, exécuter
- Owner, Group, Other
- Représenté par un vecteur de 4 valeur octale

Seulement l'owner et le root peuvent modifier les permissions.
- Cette permission ne peut pas être déléguée ou partagée.

Bits Setid - Expliqué dans quelques slides.

### Principes de designs sécurisés

Compartmentalization :
- Principe de "Least privilege" (le moins de privilège)
-  Isolation
Défense en profondeur :
- Utilisé plus qu'un système de sécurité
- Échouer de façon sécurisé
Keep It Simple (rester simple)

#### Least Privilege

Un privilège est l'a possibilité d'accéder ou de modifier une ressource.

Il faut d'abord compartimenter et isoler le système afin de limiter les intéractions entre ses compartiments.

Un module du système ne devra alors qu'avoir les privilèges minimum dont il a besoin pour les actions voulues.

##### L'isolation entre les processus

Les processus dans l'OS :
- Un processus peut avoir des fichiers d'accès, des sockets réseau, ...
	- Permissions données par rapport à l'id utilisateur
- Deux processus avec le même id utilisateur on les même permissions.

Processus et privilèges :
- Compartiments définis par l'id utilisateur
- Privilèges définis par les actions autorisés sur les ressources du système.


#### Exemple : Mail Agent

Prérequis :
- Recevoir et envoyer des emails sur le réseau extérieur
- Placer les mails arrivant dans la boite mail utilisateur locale.

Sendmail :
- Unix traditionel
- Design monolitique
- Source historique de plusieurs vulnérabilités.

Qmail :
- Design compartimenté

##### Le design de Qmail

Agent de transfert de mail (MTA en anglais)
- Remplacement à Sendmail

Isolation fonctionnelle basé sur l'isolation de l'OS
- Modules séparé qui tourne comme des "utilisateurs" séparés
- Chaque utilisateur n'a accès qu'à des ressources spécifiques

Least privilege :
- Privilèges minimaux pour chaque id utilisateur
- Seulement un programme "setuid"
	- setuid permet à un programme de changer de user id et donc de tourner en tant qu'un autre utilisateur
- Seulement un programme "root"
	- Le programme root à tous les privilèges

![[Pasted image 20231113090224.png]]

### Unix : Id utilisateur effectif pour un processus (EUID)

![[Pasted image 20231120080542.png]]
![[Pasted image 20231120080601.png]]
![[Pasted image 20231120080609.png]]
![[Pasted image 20231120080620.png]]
![[Pasted image 20231120080627.png]]
![[Pasted image 20231120080636.png]]

### SELinux

C'est une distribution Linux qui a été créé par un groupe de recherche de la NSA en collaboration avec la Secure Computing Corporation.

Basé sur une architecture forte et flexible de contrôle d'accès obligatoire basée sur l'application de type, un mécanisme développé pour la première fois pour le système LOCK.

Plus tard, son architecture a été renforcé et renommé Flask.

SELinux est un exemple de comment le MAC peut être ajouté à Linux :
	En confinant les actions au processus.
	Et en ajoutant un processus super utilisateur.

Les mécanismes de sécurité implémenté dans le système offre un support flexible pour une large variété de politique de sécurité.

## Authentification

Ce que je sais : mot de passe, question secrète, clé secrète.
Ce que je possède : carte à puce, carte bancaire, clé RSA, téléphone portable.
Ce que je suis : physique (empreinte digitale, iris, veins, visage, voix, ...) ou comportement (signature, geste, ...) 

L'association de ses méthodes d'authentification les renforce, par exemple avec l'authentification à double facteur (2FA) qui en général demande quelque chose que l'on connais (des identifiants) et que l'on possède (le téléphone portable avec un code par sms ou une requête à approuver).

### Mot de passe

Il s'agit de quelque chose de strictement personnel, difficile à trouver mais simple à retenir (**Ne surtout pas l'écrire quelque part !**).

Possède en général un nombre minimum de caractères et/ou des symboles précis requis (1 lettre minuscule/majuscule, 1 chiffre, 1 symbole, ...).

Et ne doit pas correspondre à un mot du dictionnaire.

Il faut éviter :
- Des noms/prénoms de proche
- Numéro de téléphone portable
- Nos centres d'intérêts

Dans l'idéal il doit être changé périodiquement.

Une méthode efficace est la méthode de la phrase clé où l'on s'inspire s'une citation/expression/titre de film/... et l'on en dérive un mot de passe efficace est dont on se souviendra efficacement.

![[Pasted image 20231120081946.png]]

### L'authentification par token (et autorisation)

On a 4 grandes méthode pour cela :

Kerberos
- single domain sign-on (SDSSO) protocol
- Utilise la cryptographie par clé secrète
- Les clients demandes un ticket d'authentification (TGT) au centre de distribution des clé (KDC)

OAuth2
- Un protocole d'authentification web
- Délégation : Autorise quelques tiers à accéder et modifier la donnée que je possède sur un web service donné sans donner mes credentials.
- Il faut pour cela un serveur centralisé ou une base de donnée.

OpenID-Connect
- multi domain single-sign-on protocol (MDSSO)
- Construit par dessus OAuth2

JWT (JSON Web Tokens)
- Standard ouvert pour les token basé sur le JSON
- Permet l'authentification et l'autorisation : transmis de façon sécurisé à un client non vérifié.
- Léger et facile à générer/valider
- Ne requiert pas de serveur centralisé ou de base de donnée.
- Par contre n'offre pas de système de révocation ou de raffraichissement des token.
![[Pasted image 20231120083008.png]]

Théoriquement JWT peut permettre d'étendre OAuths2 et de se connecter à un serveur l'utilisant.

### Smartcard (carte à puce)

C'est un exemple d'authentification par objet que l'on possède. C'est une méthode qui existe depuis les années 70.

L'idée est d'avoir un objet portable/léger que l'on puisse transporter avec nous et qui permette de nous identifier (donc on ne la donne à personne).

La carte permet de stocker un ou plusieurs secret et protéger cette donnée pour en empêcher la lecture quand on ne souhaite pas s'authentifier quelque part..

