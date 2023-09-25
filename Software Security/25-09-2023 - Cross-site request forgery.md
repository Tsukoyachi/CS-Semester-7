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

```ad-fail
title: 2007 : Gmail est piraté

Lorsqu'un utilisateur se connecte à gmail, s'il viste un site malicieux générera une requête considérée comme provenant de la victime.

Cette méthode à été utilisée pour envoyer l'email de l'utilisateur à l'attaquant.

Cela a permit à un attaquant de prendre le contrôle de davidairey.com (car le domaine utilisait une authentification basée sur l'email).
```

```ad-caution
title: Pas uniquement sur serveur web : attaque sur routeur
![[Pasted image 20230925115937.png | center]]

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

Quand le navigateur se connecte à une URL, il regarde en premier s'il y a des cookies important. S'il en treouve un, il enverra l'information du cookie au serveur avec une requête HTTP.

Une page web peut contenir du contenu de plusieurs site web, donc plusieurs cookies peuvent être envoyé pendant le parcours de la page.

Certaines informations persiste plus longtemps que d'autres :
- Temporaire : identification de session (nombre aléatoire)
- Durable : Identification de l'utilisateur (user ID, peut être sécurisé, intégrité et confidentialité)

![[Pasted image 20230925083854.png | center]]
```

```ad-attention
title: "Same Origin" Policy (SOP)
Lorsque l'on ouvre deux onglets d'une même page, ces deux pages vont partager le même cookie, pour rester connecté par exemple.

En réalité, chaque navigateur est associé à un domaine (constitué d'un serveur, d'un protocol et d'un port sur lequel le contenu a été téléchargé).
Si une fenêtre utilise explicitement du code externe, ce code sera exécuté sur le domaine de cette fenêtre même s'il vient d'un autre hôte.

Un script ne peut accéder qu'aux données associés à la même origine (y compris les cookies).
- Celà permet d'empêcher qu'un script hostile vienne récupérer les données d'autres pages dans le navigateur.

Il y a eu quelques problèmes de sécurité, spéciallement dans la fin des années 90 et le début des années 2000.
```


```ad-info
title: Sessions
Généralement gérée par un framework web.

Aide à distinguer entre plusieurs sessions simultanées.
Stockage de donnée :
- La session stocke des données provenant des transaction en cours (workflow, panier, login)
- Les informations peuvent être supprimé d'une session

Opérations :
- Start session
- L'id de session est créé dans le navigateur (cookie au début, écriture url plus tard)
- La donnée est stockée et gérée par le serveur web (coûteux, ne se scale pas bien)
- end session (suppression des données)

Pros/Cons : la donnée est gérée par le serveur.
```

```ad-info
title: écriture d'URL
L'url est modifiée pour :
- Stocker des paramètres (approche RESTful) 
  `http://host:port/shopping.html?sessionid=value`
- Forcer l'utilisation d'un proxy, la destination devient un paramètre.

Opération (exemple : google)
- Une requête va nous rediriger vers :
  `https://www.google.fr/url?`**&sa=**`U&`**ei=**`U -9wU-27O8Gm0AWc2IGAAQ&usg=AFQjCNEItv3EUaJHvFL_fM- _7lmX9VzCLQ`**&sig2=**`Wdr5pg0cOye893nHZJO-hw`**&bvm=**`bv.66330100,d.bGQ`

Pros/Cons : Ne peuvent pas être supprimé par le client.
```

## La guerre du Big Data...

![[Pasted image 20230925084856.png | center]]

La durée de vie d'un cookie est un gros problème pour la vie privée !
- Attributs Expires/Max-Age

L'application devrait invalidé les cookies inutiles et ne pas se reposer sur le navigateur pour le faire.

## CSRF

![[Pasted image 20230925085608.png | center]]
Ici on peut observer le chargement d'une page web et les différentes étapes de son chargement.

![[Pasted image 20230925085637.png | center]]
Ici on peut voir plusieurs requêtes pour effectuer une transaction.

Comment fonctionne les attaques CSRF ?

Détourne des fonctionnalités de base du navigateur et certains aspects d'HTTP.
- Contrôle SOP (same origin policy) et cookie

Privilégie les attaques par escalade.
On pousse le navigateur à croire que la balise/le formulaire/la requête vient de la même origine que la destination.

L'attaquant effectue des attaques à l'aveugle car il ne peut pas voir les réponses du serveur (sauf s'il combine ça a du XSS).

Les balises :
```HTML
<img src="https://bank.com/fn?param=1">
<iframe src="https://bank.com/fn?param=1">
<script src="https://bank.com/fn?param=1">
```

Les formulaires qui s'envoie automatiquement :
```HTML
<body onload="document.forms[0].submit()"> 
<form method="POST" action=“https://bank.com/fn”> 
	<input type="hidden" name="sp" value="8109"/> 
</form>
```

Les requêtes GET sont les plus dangereuses, mais toutes les requêtes sont vulnérables (même les requêtes POST).

XmlHttpRequest (Ajax)
- Normalement soumise à la SOP mais malheureusement mal gérée par la CORS (Cross-Origin Resource Sharing) qui peut mener à une libération des contraintes SOP...
- Peut également être déjoué via un proxy.

## Vue plus large du CSRF

![[Pasted image 20230925090546.png | center]]

![[Pasted image 20230925090608.png | center]]

![[Pasted image 20230925090651.png | center]]

![[Pasted image 20230925090704.png]]

## Défense basique contre le CSRF : les secrets token

Authentification persistante validée à chaque requête HTTP, dur à deviner (évidemment), envoyé au travers d'un champs caché, on évide le cookie pour éviter le vol !!
```HTML
<input type=hidden value=23a3af01b>
```

Variations :
- identifiant de session
- token indépendant de la session
- #Todo à rattraper

