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
- Requête Réponse : le nom est explicite

Pour les message queue, le workflow ressemble à ça : 
![[Pasted image 20231004141429.png | center]]


Ici MQGET récupère un message et le supprime de la file, donc seul l'un des 2 consommateur peut la lire ici.

Pour le modèle publication souscription, le workflow ressemble à ça :
![[Pasted image 20231004142058.png | center]]

Ici TGET créer une copie du message pour un consumer tout en permettant aux autres de le consommer également.

