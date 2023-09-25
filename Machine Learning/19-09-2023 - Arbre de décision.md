 ---

 Date de création : mardi 19 septembre 2023 08:22
 Matière : Machine Learning
 Enseignant : Mme. Lingrand
 Tag :

---

La semaine dernière pour le td sur les iris on a fait un seuilage à la main pour les classer.
En réalité, nous avons fait inconsciemment un arbre de décision à la main. Voici l'une des solutions qui été proposée :
![[Pasted image 20230925224510.png |center]]

Les arbres de décisions peuvent être utilisé pour la classification comme pour la régression.
Le but va être de tester des seuils par rapport aux features (valeurs) de ma donnée.

Pour de la classification on va se rapprocher d'un kd three :

![[Pasted image 20230919082551.png |center]]

On va ajouter des lignes pour séparer les classes dans notre graphes afin de les classes, ses lignes représenteront nos valeurs seuils.

Pour la régression on va essayer de construire un escalier sur lequel on estimera les valeurs :

![[Pasted image 20230925224625.png |center]]


```ad-question
title: Mais alors, quand est ce que l'arbre doit s'arrêter de grandir ?
- On pourrait le faire jusqu'à ce que tous les échantillions soit classés
- On pourrait le faire jusqu'à ce qu'il ne reste qu'une donnéée de train par feuilles de l'arbre (le problème c'est que l'algo sera surentrainé pour rien)

Il faut éviter de construire des arbres trop profond pour éviter le surrentrainement !
```

```ad-question
title: Mais alors, comment choisir une features et une valeur seuil ?
- On peut prendre une décision qui va séparer la donnée en deux ensemble de tailles équivalentes.
- On peut aussi prendre une décision qui va diminuer l'erreur globale.
```

En réalité dans ses deux questions, il n'y a pas de réponse universelle, ça dépend des cas et pour cela en terme de codes on va jouer avec les hyperparamètres de notre algorithme de création d'arbre de décision.

## L'impureté

L'impureté se mesure à une hauteur fixe et mesure la qualité d'un nœud.
Pour la mesure de l'impureté : {1,1,0,1,1} est plus pur que {0,1,0,1,1}.

Pour un arbre de classification, on va subdiviser tant que l'impureté est trop haute.

Pour un arbre de régression, par contre on va continuer de subdiviser tant que le coût est trop haut.

### L'index de GINI

 L'index de GINI : $GINI(n) = \sum\limits_{class~c}p(c|n)(1-p(c|n))=1-\sum\limits_{class~c}p²(c|n)$ 
 Ici $p(c|n)$ c'est la probabilité que l'on trouve la classe c dans le nœud n.
- Exemple si un noeud contient {0,0,1,1,1,2,2,2,2,2}
	- p(0) = 2/10 = 0.2
	- p(1) = 3/10 = 0.3
	- p(2) = 5/10 = 0.5
	- GINI = 1 - 0.04 - 0.09 - 0.25 = 0.62
- La valeur max de l'indice de GINI = 1 - $\frac{1}{nb~class}$ 
- La valeur min de l'indice de GINI = 0

Ici l'indice de GINI mesure donc l'impureté et non la pureté.

### L'entropie ou la perte en logarithme
#Todo ![[Pasted image 20230919084028.png]]

## Construire l'arbre
#Todo ![[Pasted image 20230919084146.png]]

![[Pasted image 20230919084347.png]]

Ici on compare deux arbres construit à partir d'une table de vérité. 

Le premier qui est pur à la fin est construit en commençant par découper par la valeur a puis par b à gauche et c à droite.

Le second lui n'est pas pur, on a commencé par séparer selon b puis dans les deux sous arbre on sépare par a mais cette fois ci on a deux noeuds impurs (ils possède du 0 et du 1 ensemble).

### L'élagage (ou pruning)

#Todo J'ai pas compris ce qu'il fallait noter.

## Conclusion

#Todo ![[Pasted image 20230919085025.png]]

