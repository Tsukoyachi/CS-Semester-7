---
dg-publish: "true"
dg-home: "false"
---
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
- **stub** : Il se fait passer pour le vrai objet côté client afin d'en mimiquer le comportement du vrai objet. Il se 
- **skeleton** : Il écoute en permanence les requêtes entrante afin de fournir le bon stub au client. Avant la jdk 1.2 il fallait soit même demander à générer un skeleton, sauf que l'on s'est rendu compte qu'il pouvait être générique. Il est donc automatiquement généré au besoin grace à la génération de byte code dynamique.

![[Pasted image 20230913140329.png | center]]

Ici on peut observer que comme on l'a vu plus tôt, le client va avoir besoin du stub "obd", il va donc demander au registre RMI quel skeleton le contient.

Le client demandera alors au bon skeleton le stub requis, qui le lui renverra s'il le possède.

### Implémentation d'objet remote

Les seuls méthode accessible à distance sont celle qui sont listé dans les interfaces remotes.

On va donc vouloir créer une interface spécifique qui étend `java.rmi.Remote` pour ensuite lui ajouter les méthodes requises.

```ad-bug
title: RemoteException
Toutes les méthodes remote doivent par défaut `throw java.rmi.RemoteException` parce qu'il peut y avoir un problème lié à l'intéraction entre les deux hôte.
```

```ad-attention
title: Interface Remote
L'interface devra être connue du client afin qu'il sache comment utiliser les méthodes.
```

![[Pasted image 20230913141859.png | center]]

Cette interface décrit les méthodes appelable à distance.

![[Pasted image 20230913141944.png | center]]
Quelques contraintes :
- La classe de l'objet remote devra implémenter les méthodes de l'interface. 
- La classe devra posséder un constructeur public
- Il doit également hériter de `java.rmi.server.UnicastRemoteObject`

```ad-info
title: UnicastRemoteObject
Etant donné qu'en Java l'héritage est simple, pour ne pas "griller" notre unique héritage sur notre objet remote on peut faire ceci :
`MonInterface od = UnicastRemoteObject(obj,port)`
Chaque instance sera associé à un port TCP (point d'entrée de l'objet remote), le port voulu peut être spécifié si il est différent de 0.
```

### Client d'un objet distant

Pour interagir avec un objet remote, il faut :
- Connaître en avance la/les interface de l'objet RMI.
- Le trouver, il faut obtenir un stub/proxy qui implémente l'interface et indique le socket d'entrée de l'hôte ainsi que le port où l'objet se trouve.
- L'utiliser (utiliser les méthode offertes)

RMI donne un service de nommage qui permet de trouver un objet à travers son nom => le registre RMI (RMI registry) (celui ci tourne sur la même machine que l'objet remote)
- L'objet est enregistré en utilisant un nom connu par les clients potentiel.
- Le client demandera alors une référence (un stub) de cet objet directement.

![[Pasted image 20230913143318.png | center]]
Voici un exemple d'utilisation d'un objet remote côté client.

### Localiser un objet remote

L'objet remote doit d'abord s'enregistrer dans le registre.
- Un programme lancé sur la même machine hôte que l'objet remote : rmiregistry (commande exécutable dans le bin de n'importe quelle JDK)
- On utilise le port 1099 par défaut, sinon on peut le modifier en donnant le numéro de port en paramètre

Le registre lui peut être utilisé de deux façons depuis le code Java :
- La première c'est de le lancer depuis le code : 
  ```Java
  Registry r = LocateRegistry.createRegistry(numPort)
```
- La seconde est d'en rejoindre un existant qui a pu être lancé en ligne de commande ou via un autre code Java :
  ```Java
  Registry r = LocateRegistry.getRegistry(numPort)
```

Une fois le registre lancé ou rejoins on peut y ajouter un objet RMI visible par les autres utilisateurs via un code de ce type là :
```Java
Registry r = LocateRegistry.createRegistry(1099)
InterfaceRmi obj = new InterfaceRmiImplem(...)
r.rebind("alias", obj) 
```

Il sera alors récupérable côté client avec ce code :
```Java
Registry r = LocateRegistry.getRegistry(1099)
InterfaceRmi obj = (InterfaceRmi) r.lookup("alias")
```

```ad-attention
title: Cast du résultat de lookup
Par défaut, l'objet retourné par la méthode lookup de notre objet Registry sera de type Remote et non InterfaceRmi, par conséquent il faut le cast pour ne pas avoir d'erreur à la compilation !
```


