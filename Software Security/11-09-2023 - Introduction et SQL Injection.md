---
dg-publish: "true"
dg-home: "false"
---
---

 Date de création : lundi 11 septembre 2023 08:02
 Matière : Software Security
 Enseignant : M. Roudier
 Tag : #Introduction #SoftSec #SQL 

---

![[00-CoursSecuriteLogicielle.pdf]]

![[01-WebAttacks-SQLI.pdf]]

---
## Introduction

> [!intro]
> Le but de ce cours est de comprendre la théorie derrière les attaques, voir comme cela se déroule dans la pratique. Pour à la fin comprendre la mentalité d'un attaquant afin de construire des applications plus sécurisées.
> 

```ad-info
La cybersécurité est un domaine très vaste, ce cours possède donc plusieurs suites :
- Cryptographie et sécurité
- Cyber-security
- Security and Privacy 3.0
- Sécurité dans les réseaux 
- Sécurité des applications web 
- Security for IoT, CPS and embedded systems

En effet, la sécurité est tellement vaste qu'elle touche également d'autres domaines que le simple développement logiciel :
- Le réseau
- Le système
- Le matériel
- Le logiciel
- ...
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
Many people still use passwords which are easy to guess: their first names, their initials, their host name spelled backwards, a string of characters which are easy to type in sequence.
```

## Web App Security

```ad-info
title: OWASP Top 10 Application Security Risks - 2017
• Injection
• Broken Authentication and Session Management
• Cross-Site Scripting (XSS)
• Broken Access Control
• Security Misconfiguration
• Sensitive Data Exposure
• Insufficient Attack Protection
• Cross-Site Request Forgery (CSRF)
• Using Components with Known Vulnerabilities
• Underprotected APIs
```

Après la création de nombreuse formations, depuis 2009 le nombre de vulnérabilité dans les web applications a été grandement réduit.

![[Pasted image 20230911084742.png]]

Voici un bref aperçu d'une vue système d'une web app :
![[Pasted image 20230911084445.png]]

## Injection SQL

```ad-bug
title: Injection SQL
De la donnée utilisateurs va être récupérée depuis un formulaire.
Souvent cette donnée utilisateur va directement être utilisée dans la construction d'une query SQL.

Par exemple : 
– SELECT productdata FROM table WHERE productname = ‘user input product name’;

Une attaque par Injection SQL fait donc intervenir le placement d'une query SQL dans un formulaire utilisateur.

![[Pasted image 20230920221041.png | center]]
```


> [!example] Example d'injection SQL
> ```php
> set ok = execute("SELECT * FROM Users WHERE user = '" & form("user") & "' AND pwd =
> '" & form("pwd") & "'");
> if not ok.EOF
> 	login success
> else fail;
> ```
> Est-ce que ce code est exploitable ?
> 
> Et bien oui, imaginons que `user = "' or 1=1 -- "` (URL encoded)
> Dans ce cas le script fera :
> ```php
> ok = execute("SELECT * FROM Users WHERE user = ' ' or 1=1 -- ...")
> ```
> Le "--" dit que l'on ignore le reste de la ligne lors de la compilation. Bien évidemment ici quelque chose ou vrai vaut toujours vrai donc la connexion réussira dans le script précédent.
> 
> Malheureusement, il est facile de se connecter à de nombreux site de cette façon.
> Et ce n'est pas le pire, imaginons que `user ="'; DROP TABLES Users -- "`.
> 
> On a supprimé la table Users, mais on peut un Insert, Un Delete, un Update, réinitialiser un mot de passe, ...
> 
> ![[Pasted image 20230920220842.png | center]]

Méthode pour contrer les injections SQL :
- Méthode non efficace :
	- Blacklist
- Méthode partiellement efficace :
	- Whitelist
	- Prepared Queries

```ad-info
title: Backlist
Idée : Filtrer ou assainir les mauvais méta-caractères SQL connus, tels que les guillemets simples.

Problèmes :
1. Les paramètres numériques n'utilisent pas de guillemets.
2. Les métacaractères échappés de l'URL.
3. Métacaractères codés en Unicode.
4. Il y a un fort risque d'oubli de métacaractères

Et puis même si c'est facile de retirer certains caractères, ce n'est pas le cas de tous.

Quelques exemple de cas qui ne seront probablement pas retiré avec le blacklist :
- Different case
	- SeLecT au lieu de SELECT ou encore select
- Bypass keyword removal filters
	- SELSELECTECT
- URL-encoding
	- %53%45%4C%45%43%54
- SQL comments
	- SELECT/*foo*/num/*foo*/FROM/**/cc
	- SEL/*foo*/ECT
- String Building
	- ‘us’||’er’
	- chr(117)||chr(115)||chr(101)||chr(114)
```

```ad-info
title: Whitelist
Rejeter les données qui ne correspondent pas à votre liste de caractères sûrs à accepter.
- Identifiez ce qui est bon, pas ce qui est mauvais.
- Rejeter l'entrée au lieu d'essayer de la réparer.
- Il faut toujours gérer les guillemets simples lorsque cela est nécessaire, comme dans les noms.
lorsque c'est nécessaire, comme dans les noms.

```

```ad-todo
title: Prepared Queries
Le principe c'est de précompiler une query sql en laissant des blancs uniquement pour les variables qui ne seront pas compilées à l'exécution. Empêchant donc les injections SQL.
```


D'ailleurs il existe des scanneurs de vulnérabilité aux injections SQL, c'est une liste non exhaustive bien évidemment :
- sqlmap 
- wapity
- burp suite
- mieliekoek.pl
- wpoison
- w3af
- paros
- sqlid

```ad-info
title: L'un des objectif de l'injection SQL
Le but pour l'attaquant est de récupérer des données sensible via un flux d'informations pour SQL.

Ses flux peuvent être divisés en 3 grand groupes :
- Inband : La donnée est récupéré par le même canal qui a été utilisé pour effectué pour effectuer l'injection SQL, on verra alors l'information sur la page web.
- Out-of-band : La donnée est récupérée sur un canal différent (par exemple un email avec le résultat de la query)
- Inferential : Il n'y a pas vraiment de transfert de donnée, mais le testeur pourra reconstruire l'information en envoyant certains type de requête en particulier et en observant le comportement qui survient dans la DB/sur le serveur.

```

Pour effectuer une attaque par injection sql il y a plusieurs méthodes.

- On peut effectuer une recherche par erreur, on va provoquer des erreurs pour voir si on voit une erreur :

1. Envoyer un guillemet en entrée, s'il y a une erreur l'application est vulnérable
2. Envoyer deux guillemets pour représenter littéralement ', si l'erreur disparaît alors l'application est vulnérable
3. On peut également essayer d'utiliser des strings ou des opérateurs SQL
	1. Oracle : '||'FOO
	2. MS-SQL : '+'FOO
	3. MySQL : ' 'FOO
	4. ...

![[Pasted image 20230918081418.png | center]]
![[Pasted image 20230918081448.png | center]]
![[Pasted image 20230918081504.png | center]]

![[Pasted image 20230918081527.png | center]]
![[Pasted image 20230918081543.png | center]]

- Pour effectuer une attaque par inférence (à l'aveugle)

Qu'est ce qu'on fait si l'application n'affiche pas de donnée ?
- Il y a l'utilisation d'une contre mesure typique.

L'injection peut produire un comportement détectable :
- Page web de succès ou d'échec
- Temps de réponse long ou inexistant

Quand on teste une vulnérabilité, 1=1 est toujours vrai.

Pour n'importe quel autre requête injectée, si le même résultat est retournée, la requête est également vrai.

![[Pasted image 20230918082050.png | center]]
![[Pasted image 20230918082104.png | center]]

Pour empêcher les injections SQL :
- **Ne jamais faire les requêtes SQL soit même**
- Utilisez des requêtes SQL paramétrée/préparée 
- Utilisez les relations de mapping objet (ORM) framework
	- Et du typage dans les appels de méthode