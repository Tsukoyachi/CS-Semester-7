---
dg-publish: "true"
---
---

 Date de création : lundi 16 octobre 2023 08:00
 Matière : Software Security
 Enseignant : M. Roudier
 Tag :

---

![[02-Vulns-RaceConditions.pdf]]

---

Une situation de concurrence apparaît lorsque l'on a **2 flux d'exécutions qui veulent accéder à un même objet en même temps et qu'au moins l'un de ses 2 flux essaye de changer l'état de cet objet**.

Le résultat de ce type de situation est un comportement indéterminé.

La concurrence est éliminée en mettant les opérations la provoquant **mutuellement exclusive** c'est à dire que l'on ne peut pas faire l'une si l'autre est en cours.

En général un développeur va penser qu'un ensemble d'opérations est atomique, ce qui en réalité n'est pas assuré car plusieurs mécanisme peuvent provoquer une opération pendant une autre (un scheduler comme un `setTimeout` en javascript par exemple).

Le problème est qu'un attaquant peut prendre avantage du conflit provoqué par la concurrence.

```ad-note
title: TOC(T)TOU : Time of check (to) Time of use

- Check : Vérifier qu'un prérequis est valide (par exemple une vérification de permission)
- Use : Effectuer une opération sur un objet en supposant que le prérequis est toujours valide.

Cela peut arriver sur n'importe quel système concurrent :
- La mémoire partagée
- Le système de fichier
- Les signaux
```

## La mémoire partagée

La mémoire partagées peut facilement mener à de la concurrence :
- Les threads partagent tout l'espace mémoire
- Les processus peuvent partager des zone mémoire appelé région

Dans ce cas, il faut utilisation des mécanismes de synchronisation :
- locking, semaphores
- Java :
	- `synchronized` pour les classes et les méthodes qui peuvent être concurrente (modèle Monitor)
	- type `Atomic` (java.util.concurrent.atomic.AtomicInteger, etc...)

Mieux vaut éviter la mémoire partagée :
- On peut utiliser un modèle "message-passing", il faudra quand même garder une bonne synchronisation !

Un exemple simple :

```Java

public class Counter extends HttpServlet {
	int count = 0;
	public void doGet(HttpServletRequest in, HttpServletResponse out) {
		out.setContentType("text/plain");
		Printwriter p = out.getWriter();
		count++;
		p.println(...);
		...
	}
}
```

Ici le problème c'est la ligne `count++`, en effet même si cette ligne à l'air atomic en réalité elle ne l'est pas.

Un simple cas de concurrence :
- 2 thread lise la variable count et font tous les 2 count++ et on va donc rater une incrémentation (en passant de 0 à 2 par exemple).

## Le système de fichier Unix

![[Pasted image 20231016082230.png | center]]

Ici si l'on ne revérifie pas la permission entre le if et le fopen il serait possible de modifier le fichier en le remplaçant par un pointer sur un autre fichier pour modifier un fichier auquel on a pas accès par exemple, potentiellement en utilisant le fait que l'on soit root sur ce programme par exemple.

Si l'on prends l'exemple des fichiers temporaire,  il s'agit de fichier en général situé dans /tmp ou /var/tmp qui ne nécessite pas de droit particulier pour leur création et qui en général ont des noms facilement reconnaissable.

Une attaque possible serait d'essayer de deviner le nom d'un fichier temporaire, de faire un `ln -s /etc/target fichier_tmp` qui va faire un lien symbolique entre notre fichier cible (/etc/target) et le fichier temporaire. Un programme victime qui voudrait créer le fichier_tmp nous ferait une copie de notre /etc/target. Et pour le nom du fichier temporaire si on ne le trouve pas du premier coup on peut le bruteforce !

