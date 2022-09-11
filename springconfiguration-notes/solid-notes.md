# SOLID: The First 5 Principles of Object Oriented Design (Extra #1)

Inspiration is taken from [this post](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design).

## S - Single-responsibility Principle

The first principle says:
**A class should have one and only one reason to change, meaning that a 
class should have only one job.**

It should only have one job and that job should be its purpose. The class should
not have to concern with any type of other functionality. It should remain exclusive
to the purpose for it was built. 

## O - Open-closed Principle

Open-closed Principle states:

**Objects or entities should be open for extension, but closed for modification.**

This means the class should be allowed to extend in order to make some modifying
changes but should not modify the original class. This keeps the original
functionality intact.

Coding to an **interface** is an integral part of the five principles of object
oriented programming. 

You do not want to modify the original classes but if more objects are made that
need some similar functionality, you can use interface coding in order to keep
everything in the same page and that there is no issue with future functionality. 

## L - Liskov Substitution Principle

The principle states:

**Let q(x) be a property provable about objects of x of type T. Then q(y) should
be provable for objects y of type S where S is a subtype of T.**

What the hell does this mean? This means This means that every subclass derived
from a parent class should be substitutable for their base/parent class. This is 
the component for parent/child relationships between classes. 

## I - Interface Segregation Principle
The principle states:
```text
A client should never be forced to implement an interface that it doesn't use, or
clients shouldn't be forced to depend on methods they do not use. 
```

You do not want to modify an interface and create new functionality for all classes
that it is implemented with that it doesn't need. A circle class does not need a 
volume method, neither does a square class. For this reason, the Shape interface
should not have a volume method forcing all contracted objects to adhere to it. 

## D - Dependency Inversion Principle

The principle states:
**Entities must depend on abstractions, not on concretions. It states that the high-level module must not depend on the low-level module, but they should depend on abstractions.**

Essentially, you don't want to depend on one particular class to provide the fuctionlity
that you need for the current class you are in. This is why you code to an interface
AND you make sure that any data fields will use the interface so that way it is 
abstraction that runs the show and not a specific implementation.

## Important Takeaways

Provide some flexibility for your code so that it is
still functioning after further modifications are made. Backwards compatibility is
key. 
