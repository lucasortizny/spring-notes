# Annotation Autowiring and Qualifiers (Notes #11)

## Autowiring
- Injecting FortuneService into a Coach implementation
- Spring will scan @Components 
- Any one implements FortuneService interface???
- If so, let's inject them ...oop which one?

What happens if there are multiple implementations out there? What is the strategy for choosing the implementations?

Uhmmm... we have a little problem. It will give you a problem that will look like this:
```text
Error creating bean with 'tennisCoach':
Injection of autowired dependencies failed.
```
This is caused by the ``NoUniqueBeanDefinitionException`` within Spring. Meaning that there does not exist a default one
to choose because there is more than one implementation of it. Spring will list out all the implementations of the 
classes that you have available.

The only way to get around something like this is the ``@Qualifier`` annotation. And it would look something like this:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Component;

@Component
public class TennisCoach implements Coach {
    @Autowired
    @Qualifier("happyFortuneService")
    private FortuneService fortuneService;
    //...
}
```

You want to be specific and give the bean id (in this case it is ``happyFortuneService``) in the ``@Qualifier`` tab 
in order to indicate which bean you want to inject into. 

## Injection Types supported by @Qualifier

Can apply the ``@Qualifier`` annotation to the following injection types:
- Constructor injection
- Setter injection methods
- Field injection

An important thing to note is that you need to make sure you do not have any conflicting inject-types when using the 
annotation method. Some of these like the setter injection and such will require no-arg constructor defaults and such.
 
``@Qualifier`` is a nice feature but it gets a little tricky when used with constructors. It honestly seems the 
``@Qualifier`` keyword is best used for private variables unless you want to pass it in as arguments to setter methods
or constructors. 