# The concept of object-oriented programming (OOP)

The object-oriented approach is more like a set of guiding concepts than a technical method. Specifically, there are four overarching OOP principles: _**encapsulation**_, _**inheritance**_, _**polymorphism**_, and _**reusability**_.

_**Encapsulation**_ represents the mechanism for code to bind with the data it manipulates. Only declared methods within a class can access the class data. This characteristic will prevent failures from spreading to other application components because every class is independent. Developers don't need details about the object's internals to use it effectively. Instead, they only need to know the results produced by class methods.

_**Inheritance**_ makes all properties and methods available to a child class. This characteristic allows developers to reuse common logic and model real-world relationships. Developers can use inheritance to avoid code duplication and simplify object design complexity. Inheritance supports the reusability of code to eliminate boilerplate rewriting and also helps decrease the overall code volume.

_**Polymorphism**_ means objects can adopt multiple forms depending on their context. Polymorphism helps in the dynamic calling of correct functions. This characteristic allows developers to switch implementations when needed. For example, databases can be in many ways, such as talking to a file system or an RDBMS server like MySQL or a NoSQL server like MongoDB. Using polymorphism, developers can define an interface to work with databases, and classes that implement the interface will execute the correct database calls.

_**Reusability**_ is the result of encapsulation, inheritance, and polymorphism. When developers want to create a new class, but an existing class already contains the desired code, they can derive a new class by extending the old one. In OOP, these modular classes enable developers to reuse those classes when needed, even in other applications and projects. This characteristic allows developers to perform fixed operations on particular objects and add functionality as the application and codebase evolve.
