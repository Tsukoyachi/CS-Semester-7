 ---

 Date de création : mercredi 20 septembre 2023 21:41
 Matière : Middleware
 Enseignant : Mme. Baude / M. Tigli
 Tag :

---

![[AppRepRMI-ENG.pdf]]

---

## RMI et les threads

Pour faire simple, quand un client appelle une méthode d'un objet remote, côté serveur un thread séparé se lance afin d'exécuter la méthode, cela permet à plusieurs appelant d’interagir avec l'objet RMI simultanément.

Mais là on voit le problème venir... qui dit thread dit problème d'accès concurrent à une ressource, et ça malheureusement c'est à nous développeur de le gérer.

Pour cela on a plusieurs outils (synchronized, wait, notify, sémaphores et j'en passe), on va nous en apprendre quelques uns mais je ne fais pas partie des étudiants du cours de <u>Gestion de la concurrence</u> donc je ne fournirai que des explications provenant de mon expérience concrète lors des travaux dirigés et des cours magistraux, je ne vise pas à avoir une connaissance parfaite à leurs sujets.

Bien entendu ce type d'approche avec des threads posent plusieurs soucis notables :
- Accès concurrent à une donnée, celle-ci peut être modifiée avant une lecture ou autre.
- Live-lock : 

#Todo ![[Pasted image 20230920142919.png]]
 