# Field Injection with Annotations and Autowiring (Notes #10)

Inject dependencies by setting field values on your class directly (even private fields).
This is accomplished by Java Reflection.

## Development Process - Field Injection 
1) Configure the dependency injection with Autowired Annotation

- Applied directly to the field.
- No need for setter methods.

### Step 1: configure the dependency injection with Autowired Annotation
File: TennisCoach.java

```java
import nyc.pikaboy.springdemo.FortuneService;

public class TennisCoach implements Coach {
    @Autowired
    private FortuneService fortuneService;
    
    public TennisCoach(){
        // empty constructor
    }
    // NO NEED FOR SETTER METHODS
}
```

You place ``@Autowired`` directly on the field. Behind the scenes, when Spring
creates your object, it will automatically set your field directly without having
to do any additional work using something called Java Reflection.

## Lucas' Notes

Check out [this note](compare-injectiontypes.md) for more information on the different
injection types and making the decision on which one to choose and how to invoke each of them.

