# Spring Dependency Injection with Annotations and Autowiring - Constructor Injection (Notes #8)

## Demo Example
- Our **Coach** already provides daily workouts.
- Now will also provide Daily Fortunes
- New Helper: FortuneService
- This is a **dependency**.

## What is Spring Autowiring?

- For dependency injection, Spring can also use autowiring.
- Spring will look for a class that *matches* the property. 
- *matches by type*: class or interface
- Spring will inject it automatically... hence it is **autowired**.

### Autowiring Example

- Injecting FortuneService into a Coach implementation
- Spring will scan ``@Components``.
- Any one implements FortuneService interface???
- If so, let's inject them. For example: *HappyFortuneService*. 

### Autowiring Injection Types
There are three types of injections possible with Autowiring:
1) Constructor Injection
2) Setter Injection
3) Field Injections

### Development Process - Constructor Injection

1) Define the dependency interface and class
2) Create a constructor in your class for injections
3) Configure the dependency injection with **@Autowired** Annotation. 

### Step 1: Define the dependency interface and class.
File: FortuneService.java
```java
public interface FortuneService {
    public String getFortune();
}
```
File: HappyFortuneService.java

```java
import org.springframework.stereotype.Component;

@Component
public class HappyFortuneService implements FortuneService {
    public String getFortune(){
        return "some fortune here";
    }
}
```

### Step 2: Create a constructor in your class for injections.
File: TennisCoach.java

```java
import org.springframework.stereotype.Component;

@Component
public class TennisCoach implements Coach{
    private FortuneService fortuneService;
    public TennisCoach(FortuneService fortuneService){
        this.fortuneService = fortuneService;
    }
}
```

Remember that in this scenario, we need to create a constructor that takes in all
the arguments for the dependencies we are injecting in order to actually inject
them. 

### Step 3: Configure the dependency injection using the @Autowired Annotation.
File: TennisCoach.java

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class TennisCoach implements Coach {
    private FortuneService fortuneService;

    @Autowired //this line was added here
    public TennisCoach(FortuneService fortuneService) {
        this.fortuneService = fortuneService;
    }
}
```
Note on our constructor, ``@Autowired`` is where the magic happens and the
injection happens automatically instead of the long XML file. 

**Q: What about if there is multiple implementations of the FortuneService class?**

This can be configured using the ``@Qualifier`` annotation which will be studied
about in a later set of notes. 

## Lucas' Notes

What are the potential uses for something like this? Let's say we have an object
that needs to be updated with new functionality or new things. With the dependency
injection, we can make this work. Maybe if the implementations internally of an
object changes, then it is possible for this. 

According to [stackify](https://stackify.com/dependency-injection/#:~:text=The%20dependency%20injection%20technique%20enables%20you%20to%20improve%20this%20even,code%20in%20your%20business%20logic.),
the purpose of using dependency injection is that it separates the concept of creating
the object and using the object. This means dependencies can be changed remotely. We think of the
FortuneService being a general interface and we can change which type of class is implemented
using some Spring Annotations to focus on the dependency injection. It is good to check out
the first five principles of Object-oriented Programming found [here](solid-notes.md).

It seems that ``@Autowired`` is no longer required unless you are going to use multiple constructors. 
In general it is good practice to use the annotations not just for readability sake but also for organizational
purposes. Remember: **it is only required to use it when there is multiple constructors and one needs to be specified for
dependency injections**.

