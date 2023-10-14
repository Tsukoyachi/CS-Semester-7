---
dg-publish: "true"
---
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



### Les distances 

Il ne faut pas oublier de standardiser les données sinon certaines variables auront beaucoup plus d'importance que d'autres. 

- Calculer le mean absolute deviation : $s_{j}= \frac{1}{n}\sum\limits_{i=1}^{n}|x_{ij} - \mu_{j}|$  où $\mu_{j}=\frac{1}{n}\sum\limits_{i=1}^{n}x_{ij}$ 
- Calculer la mesure standardisé (z-score) : $z_{ij}= \frac{x_{ij}-\mu_{j}}{s_{j}}$ 

Voici un exemple pour s'entraîner à faire les calculs.
![[Pasted image 20231003082308.png | center]]

Mais pourquoi standardiser les données ? Pour avoir une meilleur notion de distance :

![[Pasted image 20231003082742.png | center]]

```ad-danger
title: Distance de Manhattan
Ce sera probablement aux tests :
La distance de manhattan entre alice et bob pour la version non standardisé :
|50-70| + |11000-11100| = 120
C'est la somme des valeurs absolus des écarts entre les variables de alice et bob.
```

On voit qu'ici on observe d'énormes écart entre les distances de Manhattan non standardisé alors que pour la version standardisé on a des valeurs plus faibles mais aussi plus proche les une des autres.

![[Pasted image 20231003082817.png | center]]

La distance euclidienne c'est le cercle vert, celle de Manhattan le carré bleu, la max distance c'est le losange.

![[Pasted image 20231003083033.png]]
![[Pasted image 20231003083043.png]]


Pour les approches clustering, celle à retenir c'est le **k-Means** même si on va en voir d'autres aujourd'hui. 
![[Pasted image 20231003083141.png | center]]


## Les algorithmes de partitioning, concept de base


![[Pasted image 20231003083417.png | center]]
![[Pasted image 20231003083431.png | center]]

Un cas où ça se passe bien :
![[Pasted image 20231003083747.png | center]]

Un cas où ça se passe mal :
![[Pasted image 20231003083805.png | center]]

Il se passe mal car l'un des problèmes de k-means c'est la mauvaise initialisation.

### Avantages et Inconvénients

- Avantages
	- Relativement efficace : O(tkn) où n c'est le nombre d'objet, k le nombre de clusters et t le nombre d'itérations. Normalement k, t << n
- ![[Pasted image 20231003084429.png]]
- Faiblesse : 
	- ![[Pasted image 20231003084454.png]]

#Todo J'ai arrêté de noter pour écouter, si nécessaire go compléter ici.