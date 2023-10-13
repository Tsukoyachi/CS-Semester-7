---
dg-publish: "true"
dg-home: "true"
---
---

 Date de création : <% tp.date.now(format = "dddd DD MMMM yyyy HH:mm") %>
 Matière : Software Security
 Enseignant : M. Roudier
 Tag :

---

 <% await tp.file.move("/Software Security/" + tp.file.title) %>
 <% tp.file.rename(tp.date.now(format = "DD-MM-YYYY") + " - ") %>
