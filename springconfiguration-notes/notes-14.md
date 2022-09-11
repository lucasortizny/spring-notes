# Spring Configuration with Java Code / No XML continued: Defining Beans with Java Code

That is a long name but I think this deserves a separate notes file just for this. 

## Development  Process
- Define method to expose bean
- Inject bean dependencies
- Read Spring Java configuration class
- Retrieve bean from Spring container

### Step 1: Define method to expose bean

```java
import nyc.pikaboy.springdemo.SwimCoach;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SportConfig {
    @Bean
    public Coach swimCoach() {
        SwimCoach myswimCoach = new SwimCoach();
        return myswimCoach;
    }
}
```
The method name ``swimCoach`` is actually the bean `id` that will be registered by Spring container.
Notice that we are not using ComponentScan.

What about our dependencies?

### Step 2: Inject bean dependencies

What we do is take advantage of the ``@Bean`` tag and create a ``FortuneService`` within the config and
use the `@Bean` annotation to return the fortune service and generate it for the dependencies. This will look something
like this.

```java
import nyc.pikaboy.springdemo.SwimCoach;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SportConfig {
    @Bean
    public FortuneService happyFortuneService(){
        return new HappyFortuneService();
    }
    @Bean
    public Coach swimCoach() {
        SwimCoach myswimCoach = new SwimCoach(happyFortuneService());
        return myswimCoach;
    }
}
```
It seems here that we are gonna be using Constructor injection...? We are passing
the FortuneService into the constructor so we might have to resort to Constructor injection.

The ``happyFortuneService`` is going to be the bean `id` for this so take note the naming convention.
### Step 3: Reading the Spring configuration class.

We know this part already...

### Step 4: Retrieving the Spring bean from the Application Context

We know this part already...

## FAQs

### What are the real-world usages for this?

Let's say you have a class where you're not allowed to modify the source code,
specifically to add the ``@Component`` tag and run ``@ComponentScan`` to make your life easier.
By doing this ``@Bean`` and returning the classes you need wrapped as Beans, you have now essentially made them
just as useful as an ``@Component`` without having to touch that code at all. Very useful for if you're not
modifying prior code!



