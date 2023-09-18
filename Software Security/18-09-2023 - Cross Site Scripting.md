 ---

 Date de création : lundi 18 septembre 2023 08:03
 Matière : Software Security
 Enseignant : M. Roudier
 Tag :

---

![[01-WebAttacks-XSS.pdf]]

---

Quel est l'idée derrière une attaque par cross site scripting ?

![[Pasted image 20230918082849.png]]

#Todo Reprendre notes

Il y a trois sortes d'attaque XSS :
- Reflected XSS : Le script envoyé par l'attaquant va rajouter des éléments dans la réponse envoyé par le serveur victime au client victime en renvoyant par exemple les cookies du clients que le serveur attaquant pourra alors récupérer
  ![[Pasted image 20230918084347.png]]
- Stored XSS : Cette fois, le résultat sera stocké dans une ressource de la webapp par exemple une database.
  ![[Pasted image 20230918084448.png]]
- D'autres comme les attaque par la DOM

Le pire c'est que pour le viewer de pdf de Adobe en version <= 7.9 les pdf pouvaient exécuter des scripts javascript :
`http://path/to/pdf/file.pdf#wathever_name_you_want=javascript:code_here`

