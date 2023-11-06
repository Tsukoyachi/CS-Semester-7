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

L'encryption permet de transformer la donnée (aussi appelée plaintexts ou cleartexts) en un ciphertext.

Le ciphertext ne peut pas être lu par quelqu'un ne possèdant pas la clé de décryptage.

L'encryption est un mécanisme permettant d'assurer la confidentialité.

Principe de Kerckhoffs (1883) :
- La sécurité d'un système doit uniquement reposer sur l'ignorance de la clé.
```


### La cryptographie par clé symétrique

![[Pasted image 20231023082435.png | center]]

Il s'agit d'une méthode d'encryption où la même clef est utilisé pour l'encryption et la décryption.

**Le problème majeur de l'encryption par clé symétrique :** L'échange de la clé.
- En effet la clé doit être échangée entre 2 personnes souhaitant communiquer entre elles.

### Les approches pour l'encryption

#### Substitution Cipher

##### Mono alphabetic Cipher :

Le principe pour celui-ci est de prendre chaque lettre et de la remplacer par une autre choisie arbitrairement (cf : Codage césar ou le chiffrement par décalage)

Faiblesse : Analyse de fréquence d’occurrence des lettres (en français par exemple le "a" et le "e" apparaissent plus). Donc on va supposer que la lettre la plus présente dans le cipher text sera un "e"...

##### Poly alphabetic substitution cipher :	

Ici le principe est encore de substituer une lettre par une autre mais cette fois-ci afin de contrer la faiblesse précédente, on va introduire une clé (Dans notre photo c'est "BAND") et chaque lettre de la clé correspond à un nombre de décalage (B = index 1 donc 1 décalage, R + 1 décalage = S).

Ici la faiblesse précédente disparaît car par exemple les E ne sont pas tous encodé de la même façon.

![[Pasted image 20231023083322.png | center]]

#### Permutation Ciphers (ou Transposition Ciphers)

Le principe et de modifier l'ordre des lettres est modifié sans changer leur valeur.
La clé permet ici d'identifier une permutation.

![[Pasted image 20231023084003.png | center]]

#### Product Ciphers (Et plus précisément les Block Ciphers)

Ici on utilise une combinaison de permutations et de combinaisons. C'est les fondements de la cryptographie moderne.

L'un des plus courants est le **Block Ciphers** qui utilise deux principes :

- La **confusion** :

La relation entre le plain text P et le cipher text C en terme d'analyse statistique doit être relativement complexe à exploiter au travers de la cryptanalyse.

La technique de base : **substitution**

- La **diffusion** :

Chaque symbole du plain text P et/ou de la clé K doit influencer plusieurs symbole du cipher text C. 
La redondance du plain text doit être redistribué sur un cipher text.

La technique de base : **permutation (transposition)**.

### Quelques algorithmes qui découlent du block cipher

#### DES : Data Encryption Standard

Il a été développé par IBM et a été adopté en 1975.
- Les block cipher font 64 bits
- La clé fait 56 bit (72 057 594 037 927 936 keys, 2⁵⁶ keys)

Cet algorithme utilise le schéma de [Feistel](https://fr.wikipedia.org/wiki/R%C3%A9seau_de_Feistel) :
![[Pasted image 20231023084958.png | center]]

Dans les slides ont a deux slides parlant de l'utilisation du schéma de Feistel dans l'algorithme DES, je les copie ici :
![[Pasted image 20231023085449.png | center]]
![[Pasted image 20231023085500.png | center]]

Le problème c'est qu'un ordinateur avec 1024 processeurs tournant à 1 GHz peut explorer toutes les clé en un jour. Donc DES n'est plus sécurisé, en général on va surtout utilise Triple DES (DED ou EDE).

Le nouveau standard est : AES - Advanced Encryption Standard (2000) -> 128-256 bit keys.

#### Variantes de DES

![[Pasted image 20231023085558.png | center]]

Toutes les variantes ne se valent pas :
![[Pasted image 20231023085639.png | center]]
![[Pasted image 20231023085645.png]]![[Pasted image 20231023085653.png]]

Ici on voit que ECB est beaucoup moins efficace que CBC parce qu'on arrive encore à tirer des informations du plain text via le cipher text.

##### CBC Mode

![[Pasted image 20231023090038.png | center]]
![[Pasted image 20231023090048.png | center]]

##### CFB Mode :

![[Pasted image 20231023090343.png | center]]

##### OFB Mode :

![[Pasted image 20231023091011.png | center]]
##### Counter (CTR) Mode 

![[Pasted image 20231023090625.png | center]]

L'idée est que même si on perd une partie du message, on a juste besoin de l'indice du block et on peut récupérer le plain text original.

#### Petit retour sur le padding

![[Pasted image 20231023090759.png | center]]

En général utiliser du padding réduit l'efficacité d'un algorithme peu importe l'algorithme car ça ouvre la possibilité à des attaquants d'effectuer de la cryptanalyse.

#### Les types d'attaques

![[Pasted image 20231023091045.png | center]]

Les 4 scénarios présentés ici sont beaucoup plus courant qu'on ne le croit. La deuxième attaque a par exemple historiquement été utilisé lors de la seconde guerre mondiale pour donner un ordre d'idée.

#### L'évaluation de la sécurité

**La sécurité inconditionnelle** est équivalente à avoir un système sécurisé même face à un adversaire avec un montant illimité de temps et de ressources. 
Dans ce cas, y a t'il assez d'informations pour compromettre le système de sécurité ?

Un système sera dit **sécurisé au travers d'une complexité théorique** si on peut prouver que le système est sécurisé face à un adversaire avec des capacité polynomiale.

Une **sécurité prouvable** est équivalente à prouver que compromettre le système de sécurité est équivalent à résoudre un problème dit "difficile" (par exemple : factoriser un grand nombre entier, ou un logarithme discret).

La **sécurité calculable** (sécurité pratique) est égale à dire qu'un système est sécurisé face à un attaquant possédant un montant prédéterminé de temps et de ressources.

![[Pasted image 20231106081747.png]]
#Todo A rattraper parce que j'ai pas vraiment écouté cette slide

### Fonction Hash

Une fonction de hash lie un message M avec un message d'une longueur non déterminé que l'on nommera h(M) ou $\{M\}^ĥ$ qui a une longueur (généralement petite).

L'usage le plus courant des fonctions de hash est le stockage de mot de passe.

Les algorithmes les plus courants :
- MD5 (**NE PAS UTILISER !**)
- SHA-1 (**NE PAS UTILISER !**)
- SHA-256
- bcrypt
- scrypt
- Argon2
- ...

3 propriétés :
- Preimage resistance : Avec un output K donné, il est mathématiquement "difficile" de retrouver le message M tel que h(M) = K.
- $2^{nd}$ Preimage resistance : Avec un M donné, il est mathématiquement "difficile" de retrouver M' distinct tel que h(M) = h(M') = K.
- Collision-free : Il est mathématiquement "difficile" de retrouver M et M' distinct tel que h(M) = h(M').

On parle de MAC quand un calcul dépend d'une informations secrète (Message Authentification Code).

### La cryptographie par clé asymétrique

![[Pasted image 20231106082912.png]]

- Une encryption basé sur la difficulté de retrouver l'inverse d'une solution à un problème mathématique.
	- Bien plus coûteux qu'une encryption par clé symétrique.

- Diffie-Hellman (1977) :
	- Secret sharing : $(g^{a})^{b}=(g^{b})^{a}=g^{ab}$ mod p
- RSA : Rivest-Shamir-Adleman (1978) :
	- Solution standard aujourd'hui
	- $E_{KP}(P)=M^e$ mod n et $D_{KS}(C)=M^d$ mod n
	- Les clés KP=(e,n) et KS = (d,n) sont connecté par une relation mathématique.

####