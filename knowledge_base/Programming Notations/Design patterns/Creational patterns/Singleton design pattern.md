# Singleton design pattern
possibly my favourite design pattern by far,this design pattern is easy to implement and effective at what it does.
this design pattern lets you ensure that a class has only one instance, while providing a global access point to this instance.
## Why use the singleton pattern
### Ensure that a class has just a single instance
the most common reason for ensuring that a class has only one instance is to control the access to a shared resource, for example a database or a file
this way, whenever the user requests a new instance of the object, they always get the same instance.
>**NOTE:** this behaviour is impossible to implement with a regular constructor since a constructor call must always return a new object. instead this is usually done by a static instance attribute.

### Provide a global access point to that instance
sometimes a developer needs a single global access point (global variable)
while the singleton pattern is similar to global variables in that it offers a global access point to a data instance, it differs from global variables in the sense that no one is able to overwrite the instance
## Implementation
to implement a singleton design pattern, the developer needs to:
- make the default constructor private (to prevent the creation of new instances)
- make a static creation method that acts as a constructor, this will call the private constructor and saves the newly created object in a static field, and then all subsequent calls to this class is done via the static field, usually called get_instance
### Notes
- the static field is either created at the application startup or when the object is first needed (with the latter being the more used approach)
- the field creation usually needs to be thread safe using locks or semaphores to prevent multiple fields being created at the same time (deadlock)
- the singleton class is easy to implement and very efficient that it's sometimes the go to approach even when it's wrong or not needed, so be careful of your use case
- the most famous singleton use case is an application context.
- it could be a better approach to mark the singleton class as final/sealed to prevent people from creating children classes that may ruin the application integrity
- in most cases, the singleton class needs to have only one instance of the object, but in some cases the user needs multiple instances, this can all be handled in the ``getInstance`` method of the class.
## Structure
![[structure_singleton_design_pattern.png]]
The structure is quiet simple, declaring a static instance ``getInstance`` that returns the same instance every time it's called
The constructor should be hidden and the only way to interact with the class is through the ``getInstance`` method.
## Pseudo Code
```pseudo code
/// the class will define the `getInstance` method that lets consumers access the same instance throughout the program.
class SingletonClass is
    /// the field for storing the singleton instance
    /// should be static so that it can be directly accessed via the class
    private static field instance:SingletonClass
    /// constructor should always be private 
    /// to prevent direct construction and multiple instances
    private constructor SingletonClass() is 
        /// Some initialization code
        /// such as connection to database or opening a file
    public static method getInstance() is
	    if (SingletonClass.instance == null) then
	        acquireThreadLock() and then
	            /// ensure that the instance isn't initialized by another thread while the current thread is trying to initialize the instance.
	            if (SingletonClass.instance == null) then
	                SingletonClass.instance = new SingletonClass()
	    return SingletonClass.instance
	/// other logic that is specific to the class (could be database queries or whatnot)
```
the class is then used by retrieving the instance ``SingletonClass.getInstance``

> **NOTE:** there are multiple ways of safely creating the static instance, and it's up to the developer to chose the implementation that fits their needs, usually some programming languages provide features to make the creation easier, for example the `Lazy` class in c# which can be used to lazily initialise the instance in a thread safe way and be able to access it once needed.  

## Pros and Cons
### Pros
- being sure that the class only has a single instance.
- gaining global access point to the needed instance
- usually, the object is initialised only when it's first needed.
### Cons
- violation of the [[Single Responsibility Principle]] (solving two problems at the time)
- masking bad design (sometimes, components know too much about each other)
- needs special treatment in multi threaded environment to ensure single creation and handle multi threading data access.
- difficult to unit test because usually unit testing involves inheritance with mock object which is not possible since the constructor of the singleton class is private making the class sealed by default
## Relations with other patterns
### [[Facade Design Pattern]]
the [[Facade Design Pattern]] can be often transformed into a Singleton since in most cases a single facade object is sufficient.
### [[Flyweight Design Pattern]]
if you somehow manage to reduce all shared states of the object to just one flyweight object you could make it into a singleton, but there still exist two fundamental differences
- there should be only one Singleton object, whereas the flyweight class can have multiple instances with different intrinsic states.
- The singleton object can be mutable but the flyweight object are immutable
### [[Abstract Factory Design pattern]], [[Builder Design Pattern]], [[Prototype Design Pattern]] 
All of these design patterns can be implemented as singletons.
## Useful Links
[Singleton Refactoring guru](https://refactoring.guru/design-patterns/singleton) page
[Singleton c# Code Example page](https://refactoring.guru/design-patterns/singleton/csharp/example)
