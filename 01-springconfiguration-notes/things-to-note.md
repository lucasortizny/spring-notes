# Things to Remember about Spring (Updated Periodically)

A Spring Application needs to fulfill two requirements
- the App should be **configurable** *(annotation, XML, source)*
- Easily change the classes for another type by using best practices of assigning classes to its **INTERFACE**!
- For Maven related projects in IntelliJ, the ``applicationContext.xml`` and other related files will need to be stored in the ``resources/`` folder. This differs from the way Eclipse interprets these files to make an important note about this!!