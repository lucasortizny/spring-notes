# Compare the 3 Different Injection Types (Extra #2)
Which one should I use? Choose a style and then stay consistent in your project. Is
one injection type better than the other? It's the same functionality no matter 
which one you choose. Choose one that you feel comfortable with and then use it
in the application. You may see some blogposts written by some Spring fans but 
it ends up being something like a "religious" argumnet. Even in the Spring doc,
they state that these three injection types are the same across the board.
## Constructor Injection Type
### XML Version
- Create a dependency class that will be used to make a bean INJECTED into another bean.
- Create a constructor that takes in all the dependencies you're going to use.
- In the XML file, create a bean with an ``id`` and within the two bean tags, you
want to add ``<constructor-arg ref="idOfDependencyBean"/>``. You will need to set
multiple constructor arguments in the order the constructor presents it and provide
the respective bean for each one. 

### Annotated Version
- Within the ``<beans>`` and ``</beans>`` tag, add ``<context:component-scan base-package="path.to.packagename"/>``.
- Add the ``@Component`` tag to the top of all classes that need to be scanned. 
- Add the ``@Autowired`` tag to the top of a constructor that addresses all the dependencies
that need to be injected. 

## Setter Injection Type
### XML Version
- Create the setter methods in your class that needs injecting following the naming
convention of ``setDependencyName``. 
- In the XML configuration file, between the two ``<bean></bean>`` xml tags, you want
to use ``<property name="nameOfProperty" ref="nameOfDependencyBean"/>`` where there
will be a previously defined bean with an ``id`` you want to pass in the ``ref`` argument
of the XML file.
### Annotated Version
- Within the ``<beans>`` and ``</beans>`` tag, add ``<context:component-scan base-package="path.to.packagename"/>``.
- Add the ``@Component`` tag to the top of all classes that need to be scanned (and registered as beans).
- Add the ``@Autowired`` tag to the top of all setter methods where the method addresses all the 
dependencies that need to be injected.
## Field Injection Type
### XML Version
- This was accomplished using the properties file. The properties file can be imported by adding 
``<context:property-placeholder location="test.properties"`` to the header of the ``<beans/>`` tag.
This location is relative to the resources folder in IntelliJ.
- Use the property tag again but it'll look like ``<property name="nameOfProperty" value="${foo.nameOfProperty}"/>``.
It is important to note that this implementation uses the ``value`` keyword instead of the ``ref`` keyword since it 
reads a properties file and looks at each key-value pair instead of referencing another bean. This method modifies the 
property value directly, no setup required.

### Annotated Version
- Within the ``<beans>`` and ``</beans>`` tag, add ``<context:component-scan base-package="path.to.packagename"/>``.
- Add the ``@Component`` keyword above everything that needs to be turned into a bean and scanned by Spring.
- Add the ``@Autowired`` keyword above the fields themselves that need to be connected to a respective bean. This 
process will set the fields directly within Spring, even ``private`` fields.

## TLDR

Everything has its own way of doing things. You can choose the XML method or the Annotated method. The 
annotation method will still use the XML file but just to denote the Annotation will take precedence
instead of things written within the XML file. Choose a style and stick to it. But be wary of the different
preferences and be flexible to use either of the three. They all accomplish the **same** thing. 

