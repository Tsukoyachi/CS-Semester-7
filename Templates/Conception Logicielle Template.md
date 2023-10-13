 ---

 Date de création : <% tp.date.now(format = "dddd DD MMMM yyyy HH:mm") %>
 Matière : Conception Logicielle
 Enseignant : Mme. Blay
 Tag :

---

 <% await tp.file.move("CS-semester 7/CS-S7-publish/docs/Conception Logicielle/" + tp.file.title) %>
 <% tp.file.rename(tp.date.now(format = "DD-MM-YYYY") + " - ") %>
