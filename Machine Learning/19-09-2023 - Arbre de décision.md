 ---

 Date de création : mardi 19 septembre 2023 08:22
 Matière : Machine Learning
 Enseignant : Mme. Lingrand
 Tag :

---

La semaine dernière pour le td sur les iris on a fait un seuilage à la main pour les classer.
En réalité, nous avons fait inconsciemment un arbre de décision à la main. Voici l'une des solutions qui été proposée :

![[Pasted image 20230919082417.png]]

Les arbres de décisions peuvent être utilisé pour la classification comme pour la régression.
Le but va être de tester des seuils par rapport aux features (valeurs) de ma donnée.

Pour de la classification on va se rapprocher d'un kd three
![[Pasted image 20230919082551.png]]

On va ajouter des lignes pour séparer les classes dans notre graphes afin de les classes, ses lignes représenteront nos valeurs seuils.

Pour la régression :
#Todo rattraper la régression


```ad-question
title: Mais alors, quand est ce que l'arbre doit s'arrêter de grandir ?
- On pourrait le faire jusqu'à ce que tous les échantillions soit classés
- On pourrait le faire jusqu'à ce qu'il ne reste qu'une donnéée de train par feuilles de l'arbre (le problème c'est que l'algo sera surentrainé pour rien)

Il faut éviter de construire des arbres trop profond pour éviter le surrentrainement !
```

```ad-question
title: Mais alors, comment choisir une features et une valeur seuil ?
#Todo rattra
```

 