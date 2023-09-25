 ---

 Date de création : lundi 25 septembre 2023 13:21
 Matière : Algorithmique
 Enseignant : M. Bridoux
 Tag :

---

 ![[CM3.pdf]]
 ---
## Réduction

Nommons $L_d$ que l'on définit comme "L'ensemble des codes des machines de Turing, telle que la machine de Turing n'accepte pas son propre code" ou :

$L_{d}=\{<M>~|~M~n'accepte~pas~le~mot~<M>\}$

Celui-ci n'est pas décidable, si l'on veut s'en convaincre :

- Par l'absurde, supposant qu'une machine $M_d$ reconnaisse $L_d$. 
  Considérons alors l'entrée <$M_d$> donnée à la machine $M_d$.
  Deux cas sont possible :
	- Si $M_d$ n'accepte pas <$M_d$> alors, par définition du langage $L_d$, le mot <$M_d$> est dans $L_d$.
	  Or $M_d$ reconnait $L_d$, donc $M_d$ accepte <$M_d$>, **une contradiction**.
	- Si $M_d$ accepte <$M_d$> alors, par définition du langage $L_d$, le mot <$M_d$> n'est pas dans $L_d$.
	  Or $M_d$ reconnait $L_d$ donc $M_d$ n'accepte pas <$M_d$>, **une contradiction**.
- Dans les deux cas nous arrivons à une contradiction.
- Donc le langage $L_d$ n'est pas décidable.

```ad-note
title: Explication de la démo
En gros on imagine que l'on a une machine $M_d$ qui reconnaît le langage $L_d$.

Donc quand on évalue $M_d$ avec sont propre code:
- Soit il est reconnu est donc il ne peut pas implémenter $L_d$ car par définition $M_d$ ne reconnaît pas <$M_d$>.
- Soit il n'est pas reconnu mais dans ce cas étant donné que $M_d$ est censé reconnaître toutes les machines qui ne sont pas valide en étant évaluée avec leur propre code. Donc $M_d$ est censé accepté <$M_d$>.

Dans les deux cas on a une contradiction donc le langage n'est pas décidable.
```

```ad-info
title: Informations supplémentaire
En plus de savoir que $L_d$ n'est pas décidable, on sait que $L_d$ n'est également pas semi-décidable car lors de la démonstration précédente on a pas utilisé de propriété lié au fait que l'on supposait $L_d$ décidable, donc on aurait pu supposer $L_d$ semi décidable et arriver au même résultat.

Par ailleurs en observant le langage on observe que son complémentaire serait un langage qui reconnait toutes les machines qui accepte leur propre code et cela est semi-décidable, donc $L_d$ est co-semi-décidable.
```

### Réduction Turing

Une **réduction (many-one) Turing** du langage A au langage B est une fonction calculable
$f: \sum\limits_{A}^{*}->\sum\limits_{B}^{*}$  telle que $w\in A$ <=> $f(w) \in B$. On note $A\leq_{m}^{T}B$.

- Intuitivement, un problème A se réduit à un problème B si connaissant un algorithme pour décider/calculer B, on peut obtenir un algorithme pour décider/calculer A.
- A est alors plus facile (ou aussi facile) que B !
