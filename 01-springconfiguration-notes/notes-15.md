# Spring Configuration with Java Code / No XML continued: Injecting Values from Property Files

## Development Process

- Create Properties file
- Load Properties file into Spring configuration
- Reference values from Property files


Essentially for this, you're going to use the ``@PropertySource`` tag to define the 
location of the properties file for Spring to load it in. Then you will also
use ``@Value`` and reference the keys in the properties file just like you would
in the XML version of this process. This takes advantage of Spring's **field injection**.

This is the final notes of the Spring Configuration/Basics series. Up next is the Spring MVC.