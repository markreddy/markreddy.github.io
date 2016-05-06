---

title: Defining MVC
description: "Model, View and Controller"
tags: [blog, web, model, view, controller]
comments: true
image:
  feature: texture-feature-01.jpg
---

There are many definitions on the web of the MVC pattern’s components, so at the risk of confusing things even more, here are mine:<br><br>
**Model**  
The model represents the data/knowledge within a system. It usually comes from, but is not limited to, the data in the database and may include business logic. In reality the model should contain the information that the user wants to see on their screen.<br><br>
**View**  
The view is responsible for displaying the model on the screen. In the case of a web-app it is presented by a browser and in the Java world, it’s commonly built using JSPs.<br><br>
**Controller**  
The controller links the user, model and view together, taking a user’s request, marrying it with the appropriate model and combining the model with the appropriate view.