 ---

 Date de création : mercredi 27 septembre 2023 13:40
 Matière : Middleware
 Enseignant : Mme. Baude / M. Tigli
 Tag :

---
 ![[AppRepRMI-ENG.pdf]]
---

## Distribution de classes

RMI fait la distinction entre les objets remote et les autres.
Dans un monde parfait, les autres objet sont connus de chaque client en avance.

En réalité ce n'est pas toujours aussi simple.

Une solution existe avant de déclencher une erreur côté client, on parle de **téléchargement de classe à la demande**.
Ce mécanisme appartient à la technologie RMI, il utilise HTTP. Il permet de passer les pare feu, et il requiert un serveur HTTP qui tourne, peu importe son emplacement sur le réseau.
En réalité, on utilise le mécanisme de classpath de java qui lui permet de savoir où chercher des fichier java afin d'aller chercher le code manquant.

On va préciser dans la classe client à partir d'une annotation en Java sur quel registre RMI aller chercher le .class de la classe manquante.

![[Pasted image 20230927135331.png | center]]

Cependant pour faire cela plusieurs étapes importantes sont à suivre :
- Il faut préciser la codebase via la variable jvm : `java.rmi.codebase="http://hostWWW:portWWW/"`
- Commencer une communication http sur : `http://hostWWW:portWWW/`
- Pour ensuite pouvoir avoir la permission d'y récupérer des .class, il faut la variable jvm suivante :
  `java.rmi.server.useCodebaseOnly=false`