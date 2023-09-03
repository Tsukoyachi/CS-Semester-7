 ---

 Date de création : <% tp.date.now(format = "dddd DD MMMM yyyy HH:mm") %>
 Matière : Algorithmique
 Enseignant : M. Bridoux
 Tag :

---

 <% await tp.file.move("/Algorithmique/" + tp.file.title) %>
 <% tp.file.rename(tp.date.now(format = "DD-MM-YYYY") + " - ") %>