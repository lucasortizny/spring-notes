# Default Component Names (Notes #7)

So far we have already learned how to specify the bean ``id`` in the component annotation. A reminder of what that looks
like:

```java
@Component("thatSillyBean")
public class TennisCoach implements Coach {
    //...
}
```
The ``id`` is specified by the text within the ``@Component`` tag. 

### Spring also supports Default Bean ``id``'s

- Default bean ``id``: class name, *make the first letter lowercase*.
Example of this:
```text
TennisCoach as the Class Name -> tennisCoach as the default bean id
```
So let's take a look at an example via code.

```java
import org.springframework.stereotype.Component;

@Component
public class TennisCoach implements Coach {
    //...
}
```
The ``@Component`` tag here is defined without a specific ``id``. What this means is that the default ``id`` name is
going to be the class name with the first letter *lowercase*. This means the default bean `id` in this case is ``tennisCoach``.

**But how would we use this when retrieving beans?**

Well it is the same way that we are used to. We grab from the context and we just use the name that is implied from the 
default bean ``id``.

Example:
```java
//get the bean from the spring container.
Coach theCoach = context.getBean("tennisCoach", Coach.class);
```
In this case, Spring will scan the Components for an implementation of the FortuneService interface and then inject it
using the constructor that we defined. 


