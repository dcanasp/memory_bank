For common problems that we've all faced, you don't have to reinvent the wheel, you can use the solutions other have built.  [check more](https://refactoring.guru/design-patterns)
# creational
Mechanism to create objects, augmenting the flexibility and reusability
### singleton

Ensures a single instance of a class. An unique access point

If the instance already exists, you retrieve that one, otherwise you give a new one.

It breaks the Single responsibility [[solid principles]]. 
If there is multithreading this pattern will break your code as you have to wait for it
### Factory method

Defines an interface for creating an object, the one who implements it decides what class it should use.

A class returns the concrete implementation. these implementations should follow an interface
### abstract factory
a factory of factories. 
The abstract factory returns the internal factory, that is eventually implemented. 

An example are buttons on react native, a button could be implemented for windows, mac or android, and each of those buttons could be flat, raised, outlined...

### builder

Isolating the construction logic, sometimes you don't want all of the features that something might provide, if i create a rest API, i might want resilience, i might want telemetry, or i might not. The builder allows you to define what you want.

This is extremely useful in [[dotnet]] as the builder is used on all configuration classed.

Also useful when you have a massive constructor, instead of sending all of the parameters at the beginning you could do something like this `class.name().age().height().Build()`

It works by returning `this` on the class constructor and functions 

### prototype
When you want to clone a class at runtime, get all of the attributes from them by coping them.

It could be used as an alternative of inheritance

# structural
Storing objects in bigger classes and structures, maintaining them efficient and flexible at the same time 

### adapter 

Allows for two incompatible objects to work with each other 
There are class and object adapters

### bridge

it separates the abstraction from the implementation allowing for both to scale independently 

### decorator

allows modifying already existing objects without modifying the current one.

They are added sequentially
### facade

it provides a simplified interface

### proxy

someone in the middle that before the actual code that needs to be executed, useful for security. It's also a decorator
### composite 

creating composite objects, that don't difference between simple and compound objects. 

# Behavioral
How communication is handled between objects

### chain or responsibilities

Multiple controllers that are called one after the other, just like a middleware

### command 

converting a request as a stand alone object that can be shared between methods 

### Iterator

Allows iterating over an structure regardless of the underling structure

### Mediator

A class that handles the communication between all of the components, it avoids the chaos between all components. This could become a god class 

### Memento

Stores the previous state of objects so it could be restore later
### Observer

like a subscription, whenever the subject changes states the observers will get a new event

### state

modifying the state of an object at runtime, (stopped, running, waiting)
### strategy

defining a family of algorithms and being able to swap them at runtime

### template method

Defining the skeleton of a process in an abstract way, Whenever i do A, i will also do B and C.
The implementation is not defined yet but most do A, B and C

### visitor 

Allows the separation of the algorithm and the object that handles it
