# HelloSpringApp (Opening Project)

MAVEN DEPENDENCIES FOR THIS:
- spring-core
- spring-context (for the XML Application Context)

Spring is a way to dynamically apply class definitions (which are defined as beans) to the interface definitions in the Java code. This way you can externally define the interfaces and you don't need to worry about hardcoding. There is currently three methods of accomplishing this:
- XML Configuration file (legacy but most legacy app still use this)
- Java Annotations (modern style of doing this)
- Java Source Code (modern style of doing this)

XML Configuration
For doing the XML configuration file, you should just take the template that currently exists for the XML and define the <bean name="" class=""></bean>. The name for this is going to be what is retrieved in the method later and the class is going to be the package name class definition (think com.something.SomeClass) for pulling this information. I assume this is going to be able to be exported in some shape or form.

When doing the XML configuration in a Java class, you will want to do four steps.
- Load the spring configuration file, usually this is done as ```ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("path to context.xml")```. This code is easy because this essentially loads an XML application context from the Class Path.
- Retrieve the bean from the spring container. This is done using ```context.getBean("name of the bean", WhichInterfaceToBind.class)```. This takes a name of a bean defined in the XML configuration and then a class to bind it to (which is why interfaces are very resourceful here).
- Once this is done you can call methods on the newly defined class files through the XML App Context.
- You close the context with the ```.close()``` command. Note that if the close command is called later, it does not matter since the bean has already been binded to the existing classes.

One thing to note, we do ```.getBean``` and pass two parameters to bind it to the class so that way we avoid getting Cast Exceptions. This way, we always make sure we bind to the correct cast type. 

### Editor\'s Notes

*So these are some notes that I write after the fact. When running this in intelliJ, make sure the JDK for the project is changed to the newer version. 
When running this code in intelliJ, also make sure that there is a dedicated ```resources/``` folder. This is how maven is going to run the project within IntelliJ and will be looking for the beans and the properties file from the context of this folder. Such a strange way of running things but it makes things much neater for deployment.*