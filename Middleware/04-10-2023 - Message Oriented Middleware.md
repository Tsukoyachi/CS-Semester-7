---
dg-publish: "true"
---
 ---

 Date de création : mercredi 04 octobre 2023 13:31
 Matière : Middleware
 Enseignant : Mme. Baude / M. Tigli
 Tag :

---

![[Message Oriented Middleware (MOM).pdf]]

---

Il fallait un système permettant d'envoyer des messages de manière **asynchrone**. En effet, quelques inconvénients que l'on peut rencontrer avec des systèmes classiques sont :
- Les latences/pannes transitoires
- Les délais sur le réseau

On utilise alors des modèles de messageries, il en existe plusieurs :
- Message Queue : Un message envoyé est consommé par un **seul** client
- Publication Souscription : Un message publié est diffusé à tous les souscripteurs
- Publication souscription par le contenu : ici les message sont diffusé à certains consommateur en fonction du contenu du message.
- Requête Réponse : c'est juste du passage de message de façon asynchrone en les stockant temporairement dans une file entre un client et un serveur.

Pour les message queue, le workflow ressemble à ça : 
![[Pasted image 20231004141429.png | center]]


Ici MQGET récupère un message et le supprime de la file, donc seul l'un des 2 consommateur peut la lire ici.

Pour le modèle publication souscription, le workflow ressemble à ça :
![[Pasted image 20231004142058.png | center]]

Ici TGET créer une copie du message pour un consumer tout en permettant aux autres de le consommer également.

Pour la publication souscription en fonction du contenu, prenons une hiérarchie de topics (pas def dans le cours mais un topic représente comme ça traduction l'indique un sujet) :
![[Pasted image 20231004142411.png | center]]

![[Pasted image 20231004142446.png | center]]

Ici je peux ajouter un filtre pour récupérer les message, correspondant à un filtre précis (donné dans le message), il peut s'apparenter à un topic (exemple je veux récupérer les message sur les Voyage, ou sur les Hôtels si on prends le diagramme au dessus).

Ici je ne sais pas trop pourquoi MQGET ne supprime plus le message, ses notations change à chaque fois...

Pour le modèle requête réponse :
![[Pasted image 20231004142650.png | center]]

Ici le serveur va lire dans la file du client, qui lui va lire dans la file du serveur juste après ou inversement. C'est juste un moyen de communiquer de façon asynchrone pour ne rien perdre.

Des architectures possible il y en a plein, voir le slide pour plus de détails.