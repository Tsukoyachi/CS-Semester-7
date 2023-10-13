---
dg-publish: "false"
dg-home: "false"
---
 ---

 Date de création : <% tp.date.now(format = "dddd DD MMMM yyyy HH:mm") %>
 Matière : Gestion Comptable & financière
 Enseignant : Mme Bachelot
 Tag :

---

 <% await tp.file.move("/Gestion Comptable & financière/" + tp.file.title) %>
 <% tp.file.rename(tp.date.now(format = "DD-MM-YYYY") + " - ") %>
