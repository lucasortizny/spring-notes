# Spring Configuration with Java Annotations [Inversion of Control] (Notes #6)

This section is going to cover a lot of the same stuff we have done before, but now we are going to use
the Java annotations to do it instead of the XML method of doing it.


### What are Java Annotations?

- Special labels/markers added to Java Classes
- Provide meta-data about the classes
- Processed at compile-time or run-time for special processing.

An example of some tags:
```text
Boot
Color: Silver
Style: Jewel
Code: 1460
SKU: 10072090
Size US: 8
Size UK: 6
```

### Annotation Example

We have already seen an example of annotations already. Like in...
```java
public class TrackCoach implements Coach {
    @Override
    public String getDailyWorkout(){
        return "Run a hard 5k";
    }
}
```

When you do the ``@Override`` tag, we tell the compiler that we are overriding a method.
At compilation time, compiler will check/verify the override.

Lucas Notes: Because adding this annotation will make it check at compile-time for overriding the methods, then it is
definitely possible that this is a good way to keep things safe. If you do not override when the annotation is there, then
the compiler is going to complain.

### Why would we want to use Spring configuration with annotation?

- XML Configuration can be verbose (especially when we go up in the number of beans in the project)
- Configure your Spring beans with annotations.
- Annotations minimizes the XML configuration.

We have moving "boxes" and then we got metadata and stuff. Same thing for annotations, we add an annotation to a class
and spring will handle it from there.

### Scanning for Component Classes

- Spring will scan your Java classes for special annotations
- Automatically register the beans in the Spring container.

Spring will do a lot of work for you and scan thw classes in the background.

### Development Process

1) Enable component scanning in the Spring config file.
2) Add the @Component Annotation to your Java classes
3) Retrieve bean from Spring container.

### Step 1: Enable component scanning in config file.

In the configuration file, it is going to look something like this:
```xml
<beans>
    <context:component-scan base-package="package.name.descriptor"/>
</beans>
```

Our spring configuration file, we can remove all the beans we made in the XML file and then just add this line in order
to scan them. This happens in the background for you automatically.

### Step 2: Add the @Component to your Java classes.

When we create a Java object, we can add at the top the ``@Component`` declaration. It is going to look something like this:

```java
@Component("thatSillyCoach")
public class TennisCoach implements Coach{
    @Override
    public String getDailyWorkout(){
        return "Practice your backhand volley";
    }
}
```
The bean ``id`` in this instance is ``"thatSillyCoach"``. This will register this tennis coach automatically in Spring.
You can make it anything. It will scan and add the component annotation and register it.

### Step 3: Retrieving the bean from the Spring container.

- Same coding as before, nothing changes.

it is going to look like something like this:
```java
Coach theCoach = context.getBean("thatSillyCoach", Coach.class);
```

All you had to do was add the appropriate component to your Spring beans and it is automatically added.

## Lucas' Notes

It should be noted that this notes will continue in the myannotedversion project and the Spring notes will continue
there (to keep things organized).

**When editing XML files, make sure to keep track of which brackets use the single open and closing tags and which ones
use the open and close double tags. 
Example:
```xml
<!-- Single open and close -->
<bean />
<!-- Double open and close -->
<beans></beans>
```

Also, the base-package for the component scan is the package name where it can scan all the files for components. Take 
note of the package names (if there is no package, then it is usually just name of the project).