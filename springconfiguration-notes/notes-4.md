# Injecting Files from a Property File (Notes #4)
Purpose: when we did the literal injection in the application context file, it was injecting **HARD CODED** values. It would be better if we had a properties file and we could swap those values out as like a configuration file. *(Think the JSON implementation for the pikaboyny bot on Discord)*. This is something that can be useful for dealing with special tokens of some sort. Take note of this.

Step-by-step process:
1) Create properties file
2) Load properties file in spring config file
3) reference values from the properties file

### Create properties file
How this would look is a file ending in ``.properties``. In this example it will be ```"sport.properties"```

In the file it will be name and value pairs:
- ``foo.email=lucasortizny@github.com``
- ``foo.team=Royal Challengers Bangalore``

*You can call these names and values whatever you want!* This is just the name that will be referenced in the XML Configuration file. **Just be consistent.**

### Load Properties file in Spring config file
In the ``applicationContext.xml`` you are going to have a line that looks like this:
```<context:property-placeholder location="classpath:sport.properties"/>```

``property-placeholder`` will point to the properties file in memory.

### Reference Values from Properties File

```<property name="emailAddress" value="${foo.email}"/>```
You use the dollar sign and curly braces (this is probably the feature of java or XML that let's you put expressions within). You point it to the correct property key from the properties file and it will load it into memory.

Important thing to note: location of the properties file is relative to the XML Context file and NOT the main file. You can put relative paths or full paths but be wary the XML Context file interprets things relative to itself and NOT the file where the code is executed. 

### Editor's Notes
*The location of this file (again) will be in the ``resources/`` folder. This is the primary folder for Maven to look through so all properties files and ``context.xml`` files will need to be referenced through the relative path of the ``resources/`` folder.*