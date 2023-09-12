 ---

 Date de création : mardi 12 septembre 2023 08:05
 Matière : Machine Learning
 Enseignant : Mme. Lingrand
 Tag : #ML #Introduction 

---

Les algorithmes d'apprentissages vont être classé en deux grand groupes :
- **L'apprentissage non supervisé** (nécessite des **données** mais on a rien besoin de savoir dessus) : On va regrouper des données qui se ressemble
- **L'apprentissage supervisé** (nécessite des **données** et des **labels**) :
	- Régression : Prédiction d'une ou plusieurs valeur (On range les valeurs dans des vecteurs/matrice/tenseur si il y a plusieurs)
		- Linéaire : Essayer de tracer une droite qui passe par des points
		- Non-linéaire
		- Réseau de neurones
		- SVM
		- Arbres de décision
		- Forêt aléatoire
	- Classification
		- Régression logistique
		- Réseaux de neurones
		- SVM
		- Arbres de décision
		- Forêt aléatoire
	- Légendes, Segmentation, Compréhension (texte, oral)
- Autres modes d'apprentissage (on les verra moins cette année) :
	- Apprentissage semi-supervisé
	- Apprentissage actif
	- Apprentissage zéro exemple (ZSL) ou très peu d'exemples : On va donner une description en fonction de classes connue pour en créer une autre, ou alors on va donner seulement 1 exemple environ
	- Renforcement (données de récompenses), imitation : On va donner une récompense positif pour une réussite et une récompense négatif pour une défaite et le but est de maximiser les récompenses positives
	- Apprentissage fédéré : (Par exemple clavier android) L'algo apprend au fur et à mesure que l'on lui fourni des données en partant d'un réseau de neurones standard, le but est de ne pas avoir à fournir nos données à une société.

```ad-summary
title: Plan du cours
Lors de ce cours nous allons voir :
- Algorithme de clusturing :
	- k-means, mixture de gaussienne, hierarchiques, basés sur la densité
- Algorithmes de régression :
	- Linéaire, arbres de décisions, Réseau de neurones, ...
- Algorithmes de classification :
	- Linéaire, arbres de décisions, Réseau de neurones, ...
- Algorithmes ensemblistes
- Introduction à l'apprentissage profond
```

```ad-important
title: Partitionnement ou clustering
On par de données sans label et le but est de les regroupes en différentes classes
![[Pasted image 20230912082623.png]]

```

```ad-important
title: Régression
Régression linéaire :
![[Pasted image 20230912082729.png]]
Régression non linéaire :
![[Pasted image 20230912082830.png]]
```

```ad-important
title: Classification
Classification linéaire :
![[Pasted image 20230912082924.png]]
Classification non linéaire :
![[Pasted image 20230912083103.png]]
```

Les TD étant cours, les dataset seront souvent déjà préparé mais dans la vrai vie il y aura également une partie préparation de la données.

```ad-note
title: Séparation des données
On va séparer le dataset en 3 :
- Données pour l'apprentissage (train) :
	- Classification : Doit comporter des éléments de chaque classe
- Données de validation :
	- Afin de stopper l'apprentissage
	- Afin de choisir des hyper-paramètres
- Données de test (test) : 
	- 

```

 