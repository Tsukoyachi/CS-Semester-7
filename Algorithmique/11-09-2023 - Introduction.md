 ---

 Date de création : lundi 11 septembre 2023 13:26
 Matière : Algorithmique
 Enseignant : M. Bridoux
 Tag : #Introduction #Algorithmique

---

```ad-important
title: Definition problèmes
En informatique, un problème est une fonction f : A->B où A et B sont des ensembles dénombrable représentant des objets.

Exemples d’objets: des booléens, des graphes, des entiers, des
listes d’entiers, des fractions, etc.

Attention : Les objets doivent avoir une représentation finie, on ne peut par
exemple pas mettre en entrée ou en sortie de la fonction la liste de
tous les d´ecimales de π car celle-ci est infinie. On verra (voir TD1)
qu’on peut consid´erer que A, B ⊆ N
```

```ad-example
title: Example de problème
Exemples de problèmes informatique:
- Etant donné un entier, est-il pair? (f : Z → {⊤, ⊥})
- Le double d’un nombre n? (f : Z → Z)
- Etant donné un entier naturel, est-il premier? (f : N → {⊤, ⊥})
- Etant donnée une liste d’entiers, est-elle triée? (f : Z∗ → {⊤, ⊥})
- Quel est le minimum d’une liste d’entiers? (f : Z∗ → Z)
- Y a-t-il un chemin entre a $\in$ G et b $\in$ G dans un graphe G ?
- Etant donné un programme écrit en python, ce programme-va-t’il se terminer ou faire une boucle infinie?
```


```ad-important
title: Définition algorithme
Un algorithme est une suite finie et non ambiguë d'instructions et d'opérations.

Dans notre cas on suppose qu'un algorithme prend une entrée $a \in A$ (potentiellement inutilisée) et sort une sortie $b \in B$. 

Tous les algorithmes (qui nous int´eressent) calculent donc une
fonction et on dit donc que cette fonction est calculable. Mais, on
verra que toutes les fonctions ne sont pas calculables par un
algorithme... et on dit donc que ce sont des fonctions
non-calculables.
```

```ad-info
title: La calculabilité
La question principale de la calculabilité est: étant donné un
problème et donc une fonction f : A → B, est-ce que f est
calculable?

Remarques:
- f est calculable veut dire qu’il existe un algorithme qui calcule
- f : si on lance l’algorithme sur tout a ∈ A, on obtient f (a). En calculabilité, on ne se préoccupe pas du temps ni de l’espace m´emoire utilisé par l’algorithme pour résoudre le problème. Si f est calculable, alors on peut le prouver en exhibant un algorithme, peu importe ses performances.
- On verra des notions moins forte que calculable: semi-d´ecidable, co-semi-décidable...
```

```ad-info
title: La complexité
La question principale de la complexité est: étant donné un
problème p calculable et donc une fonction f : A → B, quelle est
la difficulté de p, c’est-à-dire quelles sont les performances du
meilleur algorithme qui peut calculer f ?

Remarques:
- On parle de performance en temps (nombre d'étapes de l’algorithme) et en espace mémoire utilisé par l’algorithme pour résoudre le problème en fonction de la taille de l’entrée.
- On prouvera donc que le problème à une difficulté bornée (par exemple un temps linéaire ou une mémoire polynomial, etc.) en exhibant un algorithme et en prouvant ses performances.
- Il est très difficile de prouver qu’un problème est réellement difficile. Mais on pourra prouver que tel problème est au moins aussi dur que tel autre (on parle de réduction).
```

Le plus compliqué est de comprendre que certaines fonctions sont non calculable, cela sera prouvé par la vidéo ci dessous :
https://www.youtube.com/watch?v=N_cDA6tF-40&feature=youtu.be

