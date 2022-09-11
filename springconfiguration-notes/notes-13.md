# Spring Configuration with Java Code / No XML (Notes #13)

Just as a reminder, there are three ways to configure a Spring container:
1) Full XML Configuration (list each bean in the XML file)
2) XML Component Scan (make use of annotations and made the XML a little smaller)
3) Java configuration class (write Java source code to configure the container, NO XML)

## Development Process
- Create a Java class and annotate as ``@Configuration``
- Add component scanning support: ``@ComponentScan`` (optional)
- Read Java configuration class
- Retrieve bean from Spring container

### Step 1: Create a Java class and annotate as ``@Configuration``

```java
import org.springframework.context.annotation.Configuration;

@Configuration
public class SportConfig {
    // ...
}
```
### Step 2: Add Component Scanning ``@ComponentScan``

```java
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan("nyc.pikaboy.springdemo")
public class SportConfig {
    // ...
}
```
You can specify where you want to scan the Components within a package.

### Step 3: Read the Spring configuration class we just created!

```java
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(SportConfig.class);
    }
}
```
We use the ``AnnotationConfigApplicationContext`` class for specifying the class where we created
our own configuration for the Spring container.

### Step 4: Retrieve Bean from the Spring container

Do it like you usually would with ``context.getBean()``.

## Lucas' Notes

``@PropertySource`` or ``@PropertySources`` helps you connect the properties file to the annotated values
that need to be inserted via the ``@Value`` annotation. It looks like this whole thing is configurable via the annotations,
which makes life much easier :o.