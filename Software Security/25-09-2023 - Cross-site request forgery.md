 ---

 Date de création : lundi 25 septembre 2023 08:21
 Matière : Software Security
 Enseignant : M. Roudier
 Tag :

---

![[03-WebAttacks-CSRF.pdf]]

---

**CSRF = Cross-site request forgery**

**Attaque CSRF** : Le navigateur d'une victime connectée envoie une requête HTTP forgée, incluant le cookie de la session de la victime et d'autres informations d'authentification.

Plus concrètement, c'est une attaque qui **force un utilisateur** à exécuter des actions non voulues sur une application web sur laquelle ils sont **déjà connecté**... Avec un peu d'aide d’ingénierie sociale (comme l'envoie d'un lien via un email ou un chat), un attaquant peut alors piéger une application web pour exécuter des actions qu'il aura précédemment choisi.

Un exemple connu :
![[Pasted image 20230925082649.png | center]]

```ad-caution
title: Pas uniquement sur serveur web : attaque sur routeur
![[Pasted image 20230925082811.png | center]]

![[Pasted image 20230925082831.png | center]]
```

```ad-note
title: Modèle d'exécution du navigateur
Dans chaque fenêtre du navigateur, on a : 
- De l'envoi de contenu web
- Du chargement de contenu web (static HTML ou dynamique script) pour afficher la page
  (cela inclut les ressources externes comme les images)
- Des réponses à des événements
  (Chargement : OnLoad | Timing : setTimeout(), clearTimeout() | Actions utilisateur : OnClick, OnMouseover, ...)
```


Maintenir l'état du client
Les interactions web sont sans état (stateless) par nature, les requêtes HTTP sont envoyé dans un sens puis dans l'autre.

Comment savoir quel navigateur se connecte ?

Quelques méthodes pour maintenir l'état :
- Cookies : browser state
- Sessions : server state
- écriture d'URL : browser state
- D'autres alternatives : cf. http://en.wikipedia/org/wiki/HTTP_cookie

```ad-info
title: Cookies
Il s'agit d'une information qu'un script peut stocker sur une machine client.
On peut l'ajouter dans le header http
- Origine et date d'expiration
![[Pasted image 20230925083639.png | center]]

Opération :
Quand le navigateur se connecte à une URL, il regarde en premier s'il y a des cookies important. S'il en treouve un, il enverra l'information du cookie au serveur avec une requête HTTP.

Une page web peut contenir
```




