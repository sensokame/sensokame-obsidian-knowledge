# Factory Method Design Pattern
this is a creational design pattern that provides an interface for creating objects in a super class but allows the subclass to alter the type of objects that will be created

## Problem
Imagine we are creating an object type, usually the bulk of the code will be inside the object class. this is all dandy, until a need arises where we need different classes that have a similar function to our original class.. this means that the two classes are related (have similar functionality) but different enough to need different classes. if we didn't have this intention in mind, a lot of refactoring will be needed.

## Solution
The Factory Method suggests replacing direct object construction calls with calls to a factory method. inside this function the objects are still created with the construction. however, the calls in the code are done with a factory method.
![[example_factor_method_subclassing.png]]
this means that in the future to create a new type, we simply need to override the factory method and not the class references.
> small limitation: the sub classes may return different types of products. to get around this, we should use the same interface between all sub classes

## Structure
![[facroty_method_structure.png]]
## Pseudo Code

```
// the creator class declares the factory method
class Dialog is 
    // the creator can provide a default implementation
    abstract method createButton():Button
    // despite the name, the creator's primary responsibility isn't creating products.
    // it usually contains some core business logic that relies on product objects
    // sub classes can indirectly change that business logic
    method render() is
        Button okButton = createButton()
        okButton.onClick(closeDialog)
        okButton.render()
// concrete creator overrides the factory method
class WindowsDialog extends Dialog is 
    method createButton(): Button is
        return new WindowsButton()

class HTMLDialog extends Dialog is
    method createButton(): Button is
        return new HTMLButton()

// the product interface declares the operations that all concrete products must implement

interface Button is
    method render()
    method onClick(f)

// concrete products provide various implementation of the interface
class WindowsButton implements Button is 
    method render (a,b) is 
        // render button in windows style
    method onClick(f) is
        // bind a native os click event.

class HTMLButton implements Button is
    method render(a, b) is
        // render a html representation of a button
    method onClick(f) is 
        // bind a web browser click event.

class Application is
    field dialog: Dialog


    // the application picks a creators type depending on the configuration
    method initialize() is 
        config = readApplicationConfigFile()

        if (config.Os == "Windows") then
            dialog = new WindowsDialog()
        else if (config.Os == "Web") then 
            dialog = new WebDialog()
        else 
            throw new Exception("Error! Unknown operating system.")


    // the client code works with an instance of a concrete creator.
    method main() is 
        this.initialize()
        dialog.render()    
```

## When to use this pattern

- when the exact types and dependencies of the objects are not known
- when providing the user with the ability of extending the internal components 
- when wanting to save system resources by reusing existing objects

## Implementation notes
- make all products follow the same interface
- add an empty factory method inside the creator class which returns a product that matches the common product interface
- when refactoring to this, find all references to product constructors and replace them with the factory method
- create set of subclass for each type, in which override the factory method and extract the appropriate bits into it
- if the factory method is empty at the end of development, it's possible to make abstract.

## Pros and Cons
### Pros
- avoiding tight coupling between creator and concrete products
- [[Single Responsibility Principle]], product creation is in one place in the program
- [[Open-closed Principle]], new types of products are introduced without breaking existing client code
### Cons
- code may become more complicated since new sub classes need to be introduced.
## Relations with other patterns
- many designed start with factory method and then move to [[Abstract Factory Design pattern]], [[Prototype Design Pattern]] or [[Builder Design Pattern]] (more flexible but more complicated)
- [[Abstract Factory Design pattern]] are often based on a set of [[Factory Method Design Pattern]], but can also use [[Prototype Design Pattern]] to compose the methods on these classes
- the [[Factory Method Design Pattern]] can be used alongside [[Iterator Design Pattern]] to let collection of sub classes return different types that are compatible with the collections
- [[Prototype Design Pattern]] isn't based on inheritance, but required more complicated initialization, [[Factory Method Design Pattern]] is based on inheritance so doesn't require more complicated initialization
- [[Factory Method Design Pattern]] is specialization of [[Template Method Design Pattern]], at the same time it may serve as a step in a large template method.

## Useful links
[factory method refactoring guru](https://refactoring.guru/design-patterns/factory-method)