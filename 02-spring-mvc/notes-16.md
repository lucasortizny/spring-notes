# Spring MVC Overview

### What is Spring MVC?

- Framework for building web applications in Java
- Based on Model-View-Controller design pattern.
- Leverages features of the core Spring Framework (Inversion of Control, Dependency Injection)

Here is how the MVC stuff works:
1) You have an incoming request coming from the Web browser
2) Then it arrives the MVC Front controller and delegates this request to a controller code (something you made).
This contains the business logic.
3) You will create a model and pass this information back to the Spring front
controller who will then insert into a View Template (think Handlebars for Node). 
4) Then this will generate a response into the browser. 

More details will be coming in the upcoming notes.

### What are the benefits of using Spring MVC?

- Spring's way of building web apps using Java
- Leverage a set of reusable UI components
- Help manage application state for web requests
- Process form data: validation, conversion, etc.
- Flexible configuration for the view layer.

