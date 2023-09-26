 ---

 Date de création : mardi 26 septembre 2023 08:19
 Matière : Machine Learning
 Enseignant : Mme. Lingrand
 Tag : #ML #PCA #tSNE 

---

 ![[PCA-tSNE.pdf]]
 ---

## Introduction

Pour n échantillions de dimensions 1 (des scalaires) : {x⁰,x¹,...,$x^{n-1}$}
- moyenne $\mu$ = $\frac{1}{n}\sum\limits_{j}x^{j}$ 
- variance var(x) = $\sigma² = \frac{1}{n}\sum\limits_{j}(x^{j} - \mu)²$
 ![[Pasted image 20230926082358.png | center]]
 Pour la dimension 2 ça ne change pas vraiment, on a :
 - $x^{j} = [x_{0}^{j},x_{1}^{j}]$ avec $0 \leq j$ < $n$
 ![[Pasted image 20230926082606.png | center]]
![[Pasted image 20230926082626.png | center]]

Ici on calcule la variance en faisant la somme des éléments diagonaux.

## PCA

L'algorithme de PCA est non supervisé, on utilise pas les labels, donc la PCA peut etre appliquée sur toutes les données car cela non changera pas le résultat des tests. On peut aussi l'appliquer uniquement sur train et l'appliquer sur le test au moment où on va utiliser les données mais ça ne change rien.

Cet algo repose sur l'analyse de la variance et de la matrice de covariance afin de réduire la dimension des données. Le but est de visualiser les données donc en dimension 2 ou 3.

C'est souvent utilisé en pré traitement des données.

![[Pasted image 20230926082944.png | center]]

![[Pasted image 20230926082959.png | center]]

Voici un exemple de ce que l'o peut voir avec la PCA :
![[Pasted image 20230926083217.png]]

Cette année on a le droit d'utiliser la librairie scikit-learn pour faire la PCA :
![[Pasted image 20230926083252.png | center]]

[Voici le lien vers la documentation scikit-learn sur l'application de la PCA sur des exemples dont un pour la visualisation en dimension 3.](https://scikit-learn.org/stable/auto_examples/ decomposition/plot_pca_iris.html)

Dans le td on essayera la PCA sur le dataset digit.

## tSNE

tSNE : tSNE : t-distributed Stochastic Neighbor Embedding

Le but de digit c'est de conserver la distance dans l'espace original et dans l'espace projeté.
Donc que les point distant reste distant et que les point proche reste proche tout en réduisant la dimension pour qu'elle soit en dimension 2 ou 3.

Donc on va d'abord calculer la distance entre chaque point 


