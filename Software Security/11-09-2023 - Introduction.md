 ---

 Date de création : lundi 11 septembre 2023 08:02
 Matière : Software Security
 Enseignant : M. Roudier
 Tag : #Introduction #Web-apps #SoftSec

---
PDF du cours :
![[00-CoursSecuriteLogicielle.pdf]]

![[01-WebAttacks-SQLI.pdf]]

---

### Les notes sont à lire en parallèle du slide étant donné qu'il ne s'agit que d'une prise de note.

#### Slide 0 : Introduction

> [!intro]
> Le but de ce cours est de comprendre la théorie derrière les attaques, voir comme cela se déroule dans la pratique. Pour à la fin comprendre la mentalité d'un attaquant afin de construire des applications plus sécurisées.
> 

```ad-summary
Voici le sommaire pour cette matière
-  Malware and Attacks: an Introduction
- Software Exploits 1: Web Apps  
- Software Exploits 2: Low level attacks 
- Basic Cryptography 
- Secure Software Development Life-Cycle 
- Secure Programming 
- Endpoint Detection and Response 
- Basic Pen-testing / Security testing
```

```ad-info
Ce cours possède une suite, il s'agit de la mineur cyber-sécurité en SI5 ainsi que d'autres cours :
- Cryptographie et sécurité
- Cyber-security
- Security and Privacy 3.0
- Sécurité dans les réseaux 
- Sécurité des applications web 
- Security for IoT, CPS and embedded systems

Le sécurité est tellement vaste qu'elle touche également d'autres domaines que le simple développement logiciel :
- Le réseau
- Le système
- Le matériel
- Le logiciel
```

```ad-hint
title: Vulnerable software
Les logiciels et systèmes informatiques ont encore plusieurs vulnérabilités.
Vocabulaire :
-> Erreur humaine 
-> fault (bug ou accès non voulu) 
-> faille de sécurité (vulnérabilité) 
-> exploitation (système compromis)

l'exploitation est aussi vieille que l'accès à distance:
- Les problèmes majeurs sont omniprésente
- L'exposition à l'accès à distance mène également à l'exploitation
```

```ad-cite
Many people still use passwords which are easy to guess: their first names, their initials, their host name spelled backwards, a string of characters which are easy to type in sequence
```


#### Slide 1 : Software exploits

