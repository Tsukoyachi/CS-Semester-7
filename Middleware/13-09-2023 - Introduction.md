 ---

 Date de création : mercredi 13 septembre 2023 13:33
 Matière : Middleware
 Enseignant : Mme. Baude / M. Tigli
 Tag : #Introduction #Middleware

---
 ![[AppRepRMI-ENG.pdf]]
---

Le but du middleware est de simplifier la vie du programmeur en intervenant entre la partie socket et des api un peu plus haut niveau. Que l'on ne voit pas forcément en tant que dev.

Par exemple quand on travaille avec une socket, faut ouvrir la socket, avec le bon port, déballer les résultats de requêtes, les décrypter...

# Intro Java Remote Method Invocation (RMI)

## Des sockets jusqu'à Java-RMI

Le but est d'avoir des applications client/serveur qui sont réparties sur plusieurs machines. Et pour que les performances soit au rendez-vous on utilise plusieurs thread pour gérer plusieurs requête à la fois.

La RMI a été  introduite il y a longtemps avec la jdk 1.1 et elle est intégrée dans le coeur de java avec des API et un support runtime.

La partie public de la RMI est dans les packages commençant par java.rmi.

Mais RMI concrètement c'est du remote protocole call (RPC) en java avec une génération de code dynamique.

La remote method invocation possède le même concept de stubs and de skeletons que l'on a pour RPC.

RMI nécessite l'utilisation de l'API de sérialization de Java qui est utilisée en général pour la persistance.

### Concepts de base

Tout d'abord on aura une différence entre les méthodes locale et les méthodes accessible à distance. Cette distinction est faite au moment de la déclaration mais également à l'utilisation mais on en reparlera plus tard.

Les objets aussi sont différencié de cette façon, un objet accessible à distance s'appelle un remote object.

- **proxy** : C'est une personne avec assez d'autorité ou de pouvoir pour agir pour quelqu'un d'autre.
- **stub** : Il représente une interface qui est vu comme le front end du remote proxy mechanism.
- **skeleton** : Il écoute en permanence les requête 

