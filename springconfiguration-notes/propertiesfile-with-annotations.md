# Quick Tutorial for Using Properties Files with Java Annotations

1) Create the properties file located in the ``resources/`` folder in IntelliJ. 
2) Add the values in the properties file as ``key=value`` pairs.
3) Add this line to the applicationContext.xml file ``<context:property-placeholder location="sport.properties"/> ``.
This will be within the ``<beans></beans>`` tags that encompass the whole xml file.
4) Finally add the ``@Value`` keyword which would be interpreted just like you normally
would. (So ``@Value("${foo.email}")`` for getting the value of the ``foo.email`` key.

Now you are done! This is how you do it via Autowiring.