# Bean Scopes with Annotations and Lifecycle Methods (Notes #12)

## Bean Scopes

Again, we are going to cover the scopes of a bean where we take a look at its lifecycle
and its type being created. 

- Scope refers to the lifecycle of the bean
- How long does the bean live?
- How many instances are created?
- How is the bean shared?

REMINDER: The default scope of a bean in Spring is a **singleton**, a bean that is only
created once and then used as a shared instance across other newly generated beans.

- It is cached in memory
- All requests for the bean will return a SHARED instance of the SAME bean.

Now how do we do this with annotations?

### Using the ``@Scope`` keyword

Take a look at the following snippet:

```java
import org.springframework.stereotype.Component;

@Component
@Scope("singleton")
public class TennisCoach implements Coach{
    // ...
}
```
You can see that in the ``@Scope`` tag, the scope of the bean is defined in quotation marks.

## Bean Lifecycle Methods

So if we recall, we had some lifecycle methods that beans automatically have and we can use these for
special purposes. 

- You can add custom code during **bean initialization**.
- This would be code such as calling business logic methods.
- Setting up handles to resources (db, sockets, file, etc).

- You can also add custom code during **bean destruction**.
- This would be code such as calling custom business logic methods.
- Clean up handles to resources (db, sockets, file, etc).

### Development Process

1) Define your methods for init and destroy.
2) Add annotations: ``@PostConstruct`` and ``@PreDestroy``.

Let's take a look at running code during the initialization of a bean.

```java
import org.springframework.stereotype.Component;

import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;

@Component
public class TennisCoach implements Coach {
    @PostConstruct
    public void doMyStartupStuff() {
        //does some things here...
    }

    @PreDestroy
    public void doMyDestroyStuff() {
        //does some cleanup in here before destruction...
    }
}
```
Take note of the annotations indicating which method is the startup method and which methods
is the destroy method.

IMPORTANT THINGS TO NOTE ABOUT LIFECYCLE METHODS: They may have any access modifier (private, public, protected).
They may have a return method but it will go unused so a lot of people end up using ``void`` for the return type.
The methods **CANNOT** take any parameters. It may have any method name you'd like.

SIDE NOTE: The ``@PreDestroy`` tag, just like its XML counterpart, will NOT be invoked when used
in the ``@Scope("prototype")`` annotation. This is just a property of the ``prototype`` scope. 

# Lucas' Notes

Ever since Java9+, this thing has changed. In order to get these tags, you need to add a 
dependency to the maven `pom.xml` file. Add the following...
```xml
<dependency>
    <groupId>javax.annotation</groupId>
    <artifactId>javax.annotation-api</artifactId>
    <version>1.3.2</version>
</dependency>
```
(Change the version number with the appropriate one at time of reading this)