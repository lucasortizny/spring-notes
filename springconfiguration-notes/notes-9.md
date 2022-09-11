# Spring Dependency Injection with Annotations and Autowiring - Setter Injection (Notes #9)

Let's remind ourselves of what the different injections types are:
1) Constructor Injection
2) Setter Injection
3) Field Injection

## Setter Injection

- We inject dependencies by calling setter methods in our class.
- Injecting FortuneService into a Coach implementation
- Spring will scan @Components
- Spring will ask: anyone implements FortuneService interface?
- If so, let's inject them (example: HappyFortuneService).

## Development Process

1) Create setter method(s) in your class for injections.
2) Configure the dependency injection with ``@Autowired`` Annotation method.

### Create setter method(s) in your class for injections.

File: TennisCoach.java

```java
import nyc.pikaboy.springdemo.FortuneService;
import org.springframework.stereotype.Component;

@Component
public class TennisCoach implements Coach {
    private FortuneService fortuneService;

    public TennisCoach() {
    }

    public void setFortuneService(FortuneService fortuneService){
        this.fortuneService = fortuneService;
    }
}
```
### Step 2: Configure the dependency injection with ``@Autowired`` Annotation Method

File: TennisCoach.java

```java
import nyc.pikaboy.springdemo.FortuneService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class TennisCoach implements Coach {
    private FortuneService fortuneService;

    public TennisCoach() {
    }

    @Autowired
    public void setFortuneService(FortuneService fortuneService) {
        this.fortuneService = fortuneService;
    }
}
```

Inject dependencies by calling ANY method on your class using ``@Autowired``. The great
thing that differentiates this from XML binding is that Annotations has the benefit
of not requiring to write ``setDailyFortuneService``. It is just going to look for 
the method that has the ``@Autowired`` on it and figures it out from there.

