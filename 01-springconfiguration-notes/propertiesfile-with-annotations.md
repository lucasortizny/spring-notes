# Quick Tutorial for Using Properties Files with Java Annotations

1) Create the properties file located in the ``resources/`` folder in IntelliJ. 
2) Add the values in the properties file as ``key=value`` pairs.
3) Add this line to the applicationContext.xml file ``<context:property-placeholder location="sport.properties"/> ``.
This will be within the ``<beans></beans>`` tags that encompass the whole xml file.
4) Finally add the ``@Value`` keyword which would be interpreted just like you normally
would. (So ``@Value("${foo.email}")`` for getting the value of the ``foo.email`` key.

Now you are done! This is how you do it via Autowiring.


## EVEN BIGGER UPDATE

If you want to do this entire thing using only Java annotations, one thing you 
can do is in the Spring configuration class that you defined, you can use the
``@PropertySource`` tag in order to define where the properties file is located
and then you can use the ``@Value`` tag in order to get away with it! Remember 
in your main application to use ``AnnotationConfigApplicationContext`` to import the
configuration we made in the configuration class. Make sure the configuration class
is denoted using the ``@Configuration`` annotation on top.