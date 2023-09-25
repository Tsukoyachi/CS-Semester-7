 ---

 Date de création : lundi 18 septembre 2023 08:03
 Matière : Software Security
 Enseignant : M. Roudier
 Tag :

---

![[02-WebAttacks-XSS.pdf]]

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

## La défense côté serveur

La meilleure façon de se protéger côté serveur c'est de valider tous les headers, cookies, string de requête, champs de formulaire, et champs caché (donc tous les paramètres) avec une spécification rigoureuse de qu'est ce qui doit être accepté (whitelist).

Le mieux est de toujours adopté une politique de sécurité positive qui spécifie ce qui est autorisé plutôt qu'une politique négative (blacklist par exemple) car elle sont dur à maintenir et sont incomplètes en général.

Pour filtrer/encoder, le mieux serait :
- De filtrer/encoder les caractères spéciaux d'HTML (par exemple &lt pour <)
- Autoriser uniquement les commandes sûres (donc pas de \<script>)
- Attention aux 'filter evastion' :
	- Regarder la cheatsheet de XSS pour les filter evasion 
	  (un exemple : `\<IMG """>\<SCRIPT>alert("XSS")...`)

Ensuite les scripts ne sont pas toujours dans des balises scripts, en effet ils peuvent se cacher dans une URI : `<img src="javascript:alert(document.cookie);">`
