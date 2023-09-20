 ---

 Date de création : mercredi 20 septembre 2023 13:36
 Matière : Middleware
 Enseignant : Mme. Baude / M. Tigli
 Tag : #RMI

---

  ![[AppRepRMI-ENG.pdf]]
 ---

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