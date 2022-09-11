# Injection of Literal Values (Notes #3)
Injecting literal values in this example will include injecting the ``emailAddress`` and the team. The process for injecting literal values is the following:
- Create setter method(s) in your class for injections
- Configure the injection in Spring config file.

### Create setter method(s) in your class for injections 

Doing this step requires that you first make private fields in the class you want to inject. We always want to use setters and getters when it comes to injecting so we keep the actual variables private.

Example: ``private String emailAddress;``
This turns into ``public void setEmailAddress(String emailAddress)...``

This will follow this kind of pattern, similar to the constructor injection.

### Configure the injection in the XML value

In the XML file, same thing you make a property but instead of making a ``ref`` (where you inject other objects), you make a ``value`` in order to inject literal values.

#### For Other Objects (Reminder): 
```<property name="fortuneService" ref="myFortuneService"/>```

#### For Injecting Literals:
```<property name="emailAddress" value="thebestcoach@luv2code.com"/>```

Again, ``ref`` is for other beans (other objects), ``value`` is for actual literals.


When coding objects into an interface, note that the restriction is going to play a role because of the interface existing functions. So while it is good practice, if we need the extra functionality we should use the actual ``CricketCoach.class`` and not ``Coach.class``.

Don't forget to close the context after opening it so no resources are wasted. 