---
layout: post
permalink: "/post/software-engineering/discovering-design-patterns"
title:  "Discovering Design Patterns"
date:   2023-06-04 07:24:19 +1100
reading_time: 6
categories: [Software Engineering, Architecture]
tags: [Design Patterns, Gang of Four, Object-Oriented Programming, Best Practices]
---

Hey there! If you read my blog about *SOLID is Basic* and wanted to explore more or simply wanted to have a refresher, then keep reading!

As a software engineer, we need to understand the importance of building robust, maintainable, and scalable software solutions. That's why I am excited to share the knowledge and insights into Design Patterns, which is *inspired* from the influential book "*Design Patterns: Elements of Reusable Object-Oriented Software*" by the **Gang of Four**.

<br/>

### What is a Design Pattern?

The book referenced the words from *Christopher Alexander* which says *"Each pattern describes a problem which occurs over and over again in our environment, and then describes the core of the solution to that problem, in such a way that you can use the solution a million times over, without ever doing it the same way twice"*

A pattern has four essential elements:

1. **Pattern name** - use to describe a design problem, it's solutions, and consequences in a word or two.

2. **Problem** - explains the problem, its context and when to apply the pattern.

3. **Solution** - describes the elements that make up the design, their relationships, responsibilities, and collaborations.

4. **Consequences** - results and trade-offs of applying the pattern.


In simple words, design patterns are customized to solve a general design problem in a particular context.

<br/>

### Describing Design Patterns

Now that we have the gist of what a design pattern is, the next question is to understand how we describe each design patterns for us to determine if it will solve the corresponding problem statement we have.

Below is the template given by the gang:

1. **Pattern Name and Classication**
    - The pattern's name conveys the essence of the pattern succintly. 
    - The pattern's classication reflects the scheme.

2. **Intent**
    - A short statement that answers the following questions: 
        - *What does the design pattern do?* 
        - *What is it's rationale and intent?*
        - *What particular design issue or problem does it address?*

3. **Also Known AS**
    - Other well-known names for the pattern, if any.

4. **Motivation**
    - A scenario that illustrates a design problem and how the class and object structures in the pattern solve the probem.
        - This scenario will help us understand the abstract description of the pattern.

5. **Applicability**
    - A short statement that answers the following questions: 
        - *What are the situations in which the design pattern can be applied?*
        - *What are examples of poor designs that the pattern can address?*
        - *How can you recognize these situations?*

6. **Structure**
    - A graphical representation of the classes in the pattern using a notation based Object Modeling Technique. Interaction diagrams to illustrate sequences of requests and collobrations between objects can also be used.

7. **Participants**
    - The classes and/or objects participating in the design pattern and their responsibilities.

8. **Collaborations**
    - How are the participants collaborate to carry out their responsibilities?

9. **Consequences**
    - A short statement that answers the following questions:
        - *How does the pattern support it's objectives?*
        - *What are the trade-offs and rsults of using the pattern?*
        - *What aspect of system structure does it let you vary independently?* 

10. **Implementation**
    - What pitfalls, hints, or techniques should you be aware of when implementing the patern? Are there language-specific issues?

11. **Sample Code**
    - Code fragments/snippet that illustrate how you might implement the pattern.

12. **Known Uses**
    - Examples of the patern found in real systems.

13. **Related Patterns**
    - A short statement that answers the following questions:
        - *What design patterns are closely related?*
        - *What are the important differences?*
        - *With which other patterns should this one be used?*

<br/>

### The Catalogue of Design Patterns

The list below are described in a high-level manner:

- **Abstract Factory**
    - Provide an interface for creating families of related or dependent objects without specifying their concrete classes.

- **Adapter**
    - Convert the interface of a class into another interface clients expect.
        - This let's classes work together that couldn't otherwise because of incompatible interfaces.

- **Bridge**
    - Decouple an abstraction from it's implementation so that the two can vary independently.

- **Builder** 
    - Separate the construction of a complex object from it's representation so that the same construction process can create different representations.

- **Chain of Responsibility**
    - Avoid coupling the sender of a request to it's receiver by giving more than one object a chance to handle the request.
        - Chain te receving objects and pass the request along the chain until an object handles it.

- **Command**
    - Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

- **Composite**
    - Compose objects into tree strucures to represent part-whole hierarchies.
        - Composite let's clients treat individual objects and compositions of objects uniformly.

- **Decorator**
    - Attach additional responsibilities to an object dynamically.
        - It provides a flexible alternative to subclassing for extending functionality.

- **Facade**
    - Provide a unified interface to a set of interfaces in a subsystem.
        - It defines a higher-level interface that makes the subsystem easier to user.

- **Factory**
    - Define an interface for creating an object, but let subclasses decide which lcass to isntantiate.
        - It let's a class defer instantiation to subclasses.

- **Flyweight**
    - Use sharing to support large numbers of fine-grained objects efficiently.

- **Interpreter**
    - Given a language, define a representation for it's grammar along with an interpreter that uses the representation to interpret sentences in the language.

- **Iterator**
    - Provide a way to access the elements of an aggregate object sequentially without exposing it's underlying representation.

- **Mediator**
    - Define an object that encapsulates how a set of objects interact
        - It promotes loose coupling by keeping objects from referring to each other explicitly, and it let's you vary their interaction independently.

- **Memento**
    - Without violating encapsulation, capture, and externalize an object's internal state so that the object can be restored to this state later.

- **Observer**
    - Define a one-to-many dependency between objects so that when one object changes state, all it's dependents are notified and updated automatically.

- **Prototype**
    - Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

- **Proxy**
    - Provide a surrogate or placeholder for another bject to control access to it.

- **Singleton**
    - Ensure a class only has one instance, and povide a global point of access to it.

- **State**
    - Allow an object to alter its behavior when it's internal state changes. The object will appear to change it's class.

- **Strategy**
    - Define a familyof algorithms, encapsulate each one, and make them interchangeable.
        - It let's the algorithm vary independently from clients that use it.

- **Template** 
    - Define the skeleton of an algorithm in an operation, deferring some steps to subclasses.
        - It allows subclasses to redefine certain steps of an algorithm without changing the algorithm's structure.

- **Visitor**
    - Represent an operation to be performed on the elements of an object structure.
        - It enables a new operation without changing the classes of the elements on which it operates.

<br/>

### Organizing the Catalogue

There are two criteria to classify a design pattern:

1. **Purpose**
    - *Creational*
        - It concerns the process of object creation.
    - *Structural*
        - Deals with the composition of classes or objects.
    - *Behavioral*
        - Characterize the ways in which classes or objects interact and distribute responsibility.

2. **Scope**
    - Specifies whether the pattern applies primarily to classes or to objects.



|   |   Creational  | Structural    | Behavioral |
------------ | ------------ | ------------ | ------------ | ------------ 
 Class |   Factory | Adapter   | Interpreter
 Object    | Abstract Factory <br/> Builder <br/> Prototype <br/> Singleton  | Adapter <br/> Bridge <br/> Composite <br/> Decarator <br/> Facade <br/> Flyweight <br/> Proxy   | Chain of Resposibility <br/> Command <br/> Iterator <br/> Mediator <br/> Memento <br/> Observer <br/> State <br/> Strategy <br/> Visitor

<br/>

### How to Select a Design Pattern

With more than 20 deisgn patterns in the catalogue, it might be overwhelming and difficult to come to a decision on which design pattern that address a particular design problem, especially if the catalogue is new and unfamiliar to us.

Below are the approaches that can help us find the design pattern that's right for our problem:

1. Consider how the design pattern solve design problems
2. Scan the Intent
3. Study how the patterns interrelate
4. Study patterns of like purpose
5. Examine a cause of redesign
6. Consider what should be variable in the design

<br/>

### How to Use a Design Pattern

Once we have come to a decision on which design pattern to use, how do we use it?

Below are step-by-step approach to applying a design pattern effectively:

1. Read the pattern once through for an overview.
    - Pay particular attention to the **applicability** and **consequences** sections to ensure the pattern is right for our problem.
2. Go back and study the Structure, Participants, and Collaborations sections.
    - Make sure we understand the classes and objects in the pattern and how they relate to one another.
3. Look at the Sample Code section to see a concrete example of the pattern in the code.
    - Studying the code helps us learn how to implement the pattern.
4. Choose names for pattern participants that are meaningful in the application context.
    - The names for participants in design paterns are usually too abstract to appear directly in an application.
        - It's useful to incorporate the participant name into the name that appears in the application. This helps make the pattern more explicit in the implementation
5. Define the classes.
    - Declare their interfaces, establish their inheritance relationships, and define the instance variables that represent data and object references.
        - Identify existing classes in our application that the pattern will affect, and modify them accordingly.
6. Define application-specific names for operations in the pattern.
    - Use the responsibilities and collborations associated with each operation as a guide.
        - Be consistent in the naming conventions.
7. Implement the operations to carry out the responsibilities and collaborations in the pattern.

<br/>

## Summary

These are just guidelines to get us started.
Over time we will develop our own unique way of working with design patterns as we progress in our journey..

We must not forget that design patterns should not be applied indiscrimantely.
Design patterns achieve flexibility and variability by introducing addition levels of indirection, and that can complicate a design and/or cost performance.

We also must not forget the principles of **KISS** (Keep It Simple Stupid) and **DRY** (Don't Repeat Yourself).


## Next Steps

If you got hooked and looking to go deeper, I would suggest to grab a copy of *Design Patterns: Elements of Reusable Object-Oriented Software* by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides. 

Happy Coding!