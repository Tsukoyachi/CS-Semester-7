 ---

 Date de création : <% tp.date.now(format = "dddd DD MMMM yyyy HH:mm") %>
 Matière : Machine Learning
 Enseignant : Mme. Lingrand
 Tag :

---

 <% await tp.file.move("/Machine Learning/" + tp.file.title) %>
 <% tp.file.rename(tp.date.now(format = "DD-MM-YYYY") + " - ") %>