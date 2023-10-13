---
dg-publish: "false"
dg-home: "false"
---
 ---

 Date de création : <% tp.date.now(format = "dddd DD MMMM yyyy HH:mm") %>
 Matière : Middleware
 Enseignant : Mme. Baude / M. Tigli
 Tag :

---

 <% await tp.file.move("/Middleware/" + tp.file.title) %>
 <% tp.file.rename(tp.date.now(format = "DD-MM-YYYY") + " - ") %>
