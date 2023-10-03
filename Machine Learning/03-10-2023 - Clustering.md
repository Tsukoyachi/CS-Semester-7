 ---

 Date de création : mardi 03 octobre 2023 08:08
 Matière : Machine Learning
 Enseignant : Mme. Lingrand
 Tag :

---

![[clustering.pdf]]

---

Le clustering est un autre algorithme de partitionnement, celui-ci est non supervisé

Des clusters sont des collections de données possédant des similarités. Ils utilisent une notion de distance entre objet (et entre groupe) pour faire ses clusters.

Un bon cluster est un cluster ayant une grande similarité inter élément à l'intérieur et une faible similarité inter élément avec les éléments à l'extérieur.
### Un exemple

Comment classifieriez vous des images de ses 6 classes ?
- muffin
- bagel
- poulet frit
- chihuahua
- labrador
- chiot

On séparerait peut être en deux cluster : Nourriture et chien

![[Pasted image 20231003081714.png | center]]


Il ne faut pas oublier de standardiser les données sinon certaines variables auront beaucoup plus d'importance que d'autres. 

- Calculer le mean absolute deviation : $s_{j}= \frac{1}{n}\sum\limits_{i=1}^{n}|x_{ij} - \mu_{j}|$  où $\mu_{j}=\frac{1}{n}\sum\limits_{i=1}^{n}x_{ij}$ 
- Calculer la mesure standardisé (z-score) : $z_{ij}= \frac{x_{ij}-\mu_{j}}{s_{j}}$ 

Voici un exemple pour s'entraîner à faire les calculs.
![[Pasted image 20231003082308.png | center]]

Mais pourquoi standardiser les données ? Pour avoir une meilleur notion de distance :

![[Pasted image 20231003082355.png]]

```ad-danger
title: Distance de Manhattan
Ce sera probablement aux tests :
La distance de manhattan entre alice et bob pour la version non standardisé :
|50-70| + |11000-11100| = 120
C'est la somme des valeurs absolus des écarts entre les variables de alice et bob.
```

On voit qu'ici on observe d'énormes écart entre les distances de manhattan 