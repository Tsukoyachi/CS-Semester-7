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

