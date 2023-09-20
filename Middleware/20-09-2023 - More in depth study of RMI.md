 ---

 Date de création : mercredi 20 septembre 2023 13:36
 Matière : Middleware
 Enseignant : Mme. Baude / M. Tigli
 Tag : #RMI

---

  ![[AppRepRMI-ENG.pdf]]
 ---

# RMI et le passage de paramètre

Pour le RMI, le but est de cacher la distribution.
Mais pour RMI on voudrait donc manipuler les paramètre de la même façon que pour Java... c'est à dire que le passage de paramètre soit fait par copie de valeur pour les types primitifs et par référence pour les objets.

Deux exemples simples pour démontrer le comportement usuel en Java :
```Java
public void foo(int a) {
	a += 1;
}

int x = 10;
foo(x);
System.out.println(x); // 10
```

```Java
public class MonInt {
	public int i;
	...
}

public void foo(MonInt a) {
	a.i += 1;
}

MonInt x = new MonInt(10);
foo(x);
System.out.println(x.i); // 11
```

Mais est-ce que l'on peut faire la même chose avec RMI ?

Pour les valeurs primitives, le passage par copie est simple, lorsque l'on envoie le paramètre par le réseau, la valeur est copié. C'est le rôle du stub de faire ses copies.

Par contre pour les objet c'est un peu plus compliqué de les copier... 

- En effet pour envoyer la valeur de l'objet à travers le réseau, il faut que celui-ci soit serializable.

- Et passer un objet par référence est également requis et RMI le permet uniquement pour les objets remote. Parce que qu'est ce qu'une référence pour un objet distant ? Il s'agit de son **stub** ! La solution est don de copier le stubs de l'objet qui lui est serializable.

- Sinon on peut également passer un objet par copie profonde mais c'est très fastidieux de le faire à la main, solution est donc d'utiliser la serialization API dont on vient de parler.

## La serialization

C'est un mécanisme générique qui transforme un graphe objet en stream de bits.
L'objet passé en paramètre est donc transformé en tableau, et ce sera le cas de tous les objet qu'il référence. C'est un processus récursif d'où le nom de copie "profonde".

Le comportement classique :
- Encoder le nom de classe
- Encoder les valeurs des attributs

```ad-danger
title: Les cycles
Si jamais un objet A dans ses attributs référence un objet B qui référence lui même l'objet A on va :
- Encoder l'objet A
- Encoder l'objet B
- Lorsque l'on trouvera la ref de l'objet A dans B on mettra juste un lien vers l'encodage de A.
```


## La déserialization

Il s'agit de l'opération inverse à la serialization (opération de décodage) qui transformera le stream de bits en objet. 

Le comportement classique :
- Lis le nom de classe
- Créé une instance d'objet de la classe, bien entendu le .class doit être connu de l'autre côté.
- Lis toutes les valeurs des attributs depuis le stream et modifie leur valeur dans la nouvelle instance.


## Implémentation de la serialization

Par défaut un objet Java n'est pas serializable, il faut implémenter une interface qui se nomme `java.io.Serializable`.

S'il n'arrive pas à se serializer il lancera une exception : `NotSerializableException`.

Pour qu'un attribut soit ignoré lors de la serialization on ajoute le mot clé `transiant`.
```Java
private transiant int iWontBeSerialized;
```

La RMI utilise par défaut l'implémentation de Serializable pour effectuer la copie des objet lorsque l'objet est Serializable. Mais le développeur peut également l'utiliser via deux méthodes simples :
```Java
  private void writeObject(ObjectOutputStream output) throws IOException
  private void readObject(ObjectInputStream input) throws ClassNotFoundException,IOException
```

Bien entendu il est possible d'override ses deux méthodes pour en changer le comportement. 
Il est possible d'en changer le comportement de la façon de notre choix, mais ses deux méthodes par défaut utilise les streams et sont en FIFO (first in first out), il faut donc que la lecture et l'écriture se face dans le même sens.
Et bien entendu la lecture et l'écriture sont symétrique, il faut donc lire tout ce que l'on écrit.

#Todo ![[Pasted image 20230920142801.png]]

# RMI et les threads

#Todo ![[Pasted image 20230920142919.png]]