 ---

 Date de création : <% tp.date.now(format = "dddd DD MMMM yyyy HH:mm") %>
 Matière : Gestion Comptable & financière
 Enseignant : Mme Bachelot
 Tag :

---

 <% await tp.file.move("CS-semester 7/CS-S7-publish/docs/Gestion Comptable & financière/" + tp.file.title) %>
 <% tp.file.rename(tp.date.now(format = "DD-MM-YYYY") + " - ") %>
