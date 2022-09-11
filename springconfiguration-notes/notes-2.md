# Dependency Injection (Notes #2)

One component of spring is *dependency injection*. According to the textbook definition, this is the dependency inversion principle; which is the client delegates to calls to another object the responsibility of providing its own dependencies.

Essentially this means the object factory that is defined in spring is in charge of injecting all the dependencies in the objects so that it just works. This fulfills the two components for Spring container:
1) Create and manage objects **(Inversion of Control)**
2) Inject object's dependencies **(Inversion of Dependencies)**

There are many types of way to inject dependencies in Spring but the two most common way are:
- **Constructor Injection**
- **Setter Injection**

Auto-wiring of beans will happen in the annotation section of the course.
### Constructor Injection
Ways of going about this: you want to make a constructor that takes in parameters so that way it is injected via the constructor.

After creating the constructor, you go into the XML file and define a bean for the class you are going to be depending on. Then in the parent class object where it will need the dependency injected in the XML, add ```<constructor-arg ref="idOfDependBean"/>```. This ``id`` will be the same ``id`` as the one you defined when assigning the bean in the configuration XML file. **WRITE THIS BETWEEN THE TWO BEAN XML TAGS, NOT IN THE OPENING BEAN BRACKET.**

Remember the deployment process for this:
1) Define the dependency interface and class
2) Create a constructor in your class for injection
3) Configure the dependency injection in the Spring config XML file.

Helper objects will need to be injected and this is the way of doing it.

### Setter Injection

For doing dependency injections through the setter, you need to do the following:
- Create setter method(s) in your class for injections
- Configure the dependency injection via the Spring XML Configuration File.

One thing to note is that Spring is going to be looking for the ```setBeanId``` method in the class so that is how it maps it one-to-one to the property whose ``id`` is beanId. ``beanProperty`` -> ``setBeanProperty``, etc. This mapping is what allows the *setter Injection*.
