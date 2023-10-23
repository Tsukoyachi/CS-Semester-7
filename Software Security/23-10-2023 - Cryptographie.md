---
dg-publish: "true"
---
---

 Date de création : lundi 23 octobre 2023 08:02
 Matière : Software Security
 Enseignant : M. Roudier
 Tag : #SoftSec #Cryptography

---

![[03-ArchiCryptoControleAccesv2-Crypto.pdf]] 

---

## Introduction

Les contrôles d'accès et la cryptographie ont pour objectif la triade CIA, on ne parle pas ici de la CIA que l'on connait tous mais d'un acronyme pour **Confidentiality, Integrity, Availability** :
- Confidentialité : Un utilisateur non autorisé ne peut pas lire information
- Intégrité : Un utilisateur non autorisé ne peut pas altérer l'information
- Disponibilité : Les utilisateurs autorisés peuvent toujours accéder à l'information

D'après l'ITU-T-X-800 (Contexte OSI) :
- La confidentialité concerne :
	- Les informations
	- Les traffics réseau
- L'intégrité concerne :
	- La donnée
	- Le programme et ses exécutions
- L'autorisation / contrôle d'accès empêche les accès non autorisé
- La non répudiation (empêche le déni à posteriori d'une transaction) avec une preuve d'origine et de livraison. (Le but est d'empêcher quelqu'un de réfuter une opération en disant qu'il n'en est pas à l'origine.)

#### Comment réaliser ses objectifs de sécurité ?

Il y a 3 approches principales :
- La prévention : Colmater des brèches de sécurité
- La détection : Détecter les brèches de sécurité
- La réaction : Réparer les dégâts et repousser les attaquants

**Attention : Une bonne prévention ne rendent pas superflus la détection et la réaction !!!**

### Mécanismes de sécurité

- La cryptographie : 
	- C'est un moyen de réduire la possibilité d'attaques survenant sur la donnée.
	- C'est également utilisé sur les algorithmes de contrôle d'accès
- Le contrôle d'accès logique et les architectures de sécurité
	- Pour les dangers liés à des utilisateurs malveillants
	- Création et défense d'un périmètre
	- Protection de la donnée et des accès
	- Modèle de contrôle d'accès (par exemple : un contrôlé d'accès basé sur les rôles)
- Les langages basés sur la sécurité
	- Pour les dangers liés à des programmes malveillant
		- *Le typage, la sécurité mémoire, les modules, les packages...*
	- Par exemple : Java, .NET/C#, Rust

## La cryptographie : Encryption, Fonction Hash, Certificats

```ad-info
title: Encryption

L'encryption permet de transformer la donnée (aussi appelée plaintexts ou cleartexts)

```
