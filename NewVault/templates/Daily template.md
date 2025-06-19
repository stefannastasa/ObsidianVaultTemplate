---
creation date: <% tp.file.creation_date() %>
modif date: <% tp.file.last_modified_date("Do MMM, YYYY") %>
modif time: <% tp.file.last_modified_date("HH:mm") %>
---
<%* 
await tp.file.move("daily/" + tp.date.now("Do MMM, Y"));
%>




