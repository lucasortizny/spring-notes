# Bean Scopes and Bean Lifecycle (Notes #5)

Some things that we need to think about:
1) Scope refers to the lifecycle of the bean
2) How long does the bean live?
3) How many instances are created?
4) How is the bean shared?

The default scope of the bean is a singleton. 

### What is a singleton?
- Spring container only creates one instance of the bean, by default.
- It is cached in memory.
- All requests for the bean will return a **SHARED** instance to the **SAME** bean.

Lucas Notes: This is pretty good for saving memory very carefully. But it is important to note all of the limitations
for this kind of thing. Shared instances mean what is done from one end will be reflected on the other.

The best use of the singleton scope is for a stateless-bean, which is a bean where you don't need to maintain in a
particular state.

You can explicitly define a bean scope by doing something like the following:
```xml
<bean id="myCoach"
      class="com.pathto.Coach.class"
      scope="singleton">
    ... Something in between...
</bean>

```
We do this by utilizing the ``scope`` parameter in the opening bean bracket and defining it in writing.

Here is a general breakdown of the bean scopes you can use.

- ``singleton``: create a single shared instance of the bean. Default scope.
- ``prototype``: create a new bean instance for each container request
- ``request``: Scoped to an HTTP web request. Only used for web apps.
- ``session``: Scoped to an HTTP web session. Only used for web apps.
- ``global-session``: Scoped to a global HTTP web session. Only used for web apps.

When you use the prototype scope, just think of the ``new`` keyword because it is going to create a NEW object completely
everytime you make a request to generate an object from the ``context.xml``.

### Bean Lifecyle Methods

Let's talk about the bean lifecycle. Here is how it usually goes in the following order:
1) Container Started
2) Bean instantiated
3) Dependencies injected
4) Internal Spring Processing
5) Your Custom Init method
6) Bean is ready for use!
7) At some point your container is shutdown
8) Your Custom Destroy Method is called.

You can add your own custom code during **bean initialization**.
- This includes calling custom business logic methods.
- Setting up handles to resources (db, sockets, file, etc).

You can add custom code during **bean destruction**.
- Calling custom business logic method.
- Clean up handles to resources (db, sockets, file, etc).

During the bean lifecycle, you can actually have spring call some of your custom code during the creation or deletion of 
beans and this is called *hooks*.

### Init: Method configuration

When setting this up in the context xml file, you can use the ``init-method`` parameter for the ```<bean />``` tag.

Here is an example of how this would look.
```xml
<beans>
    <bean id="myCoach"
          class="myversion.BaseballCoach"
          init-method="doMyStartupStuff">
    </bean>
</beans>
```

Important thing to note from this example is the ``init-method`` parameter that is in the opening tag for the bean. This
method name can be any method name. 

We can also do a similar thing for the destroy method. This is how it would look:
```xml
<beans>
    <bean id="myCoach"
          class="myversion.BaseballCoach"
          destroy-method="doMyCleanupStuff">
    </bean>
</beans>
```
Again, the way this is gonna work is a two-step process (we love making step-by-step to-dos).
1) Define your methods for init and destroy
2) Configure the method names in the Spring config file.

### What should the method look like?

- The **access modifier** can be any (public, protected, default, private).
- The **return type** can have any return type BUT you will not be able to capture the value of it. So just use "void".
- The method name can be any name.
- The method cannot have any arguments. It should be no-arg.

## Important Note about Prototype Beans

The beans that have the scope of ``prototype`` are constantly made differently and never return the same shared instance in memory.
This scope also calls the initialization methods but **NEVER** calls the destroy method. This is because after creating the
object, it does not take note of any other aspect of the object after it and so **MAKE SURE TO CLEAN UP THE RESOURCES USED 
SINCE SPRING WON'T BE ABLE TO WITH THIS SCOPE**. Every other scope can have both ``init-methods`` and ``destroy-methods`` called by Spring.

This aspect applies to both XML configurations and Annotation based configurations so be wary of the prototype scope's 
distinctive features. If you need to see the prototype object utilize the destroy method, custom coding is done and an 
example can be found [here](https://drive.google.com/open?id=1262cK04FYe7x3blpp2wVv7gmkvRyA_cX). If you want the appropriate
link to the Udemy explanation of this, check it out [here](https://www.udemy.com/course/spring-hibernate-tutorial/learn/lecture/5809260#overview).
