# Abstract Factory Design Pattern
This is a creational design pattern that lets you produce families of related objects without specifying their concrete classes

## Problem
Imagine creating object types; but each type can have multiple variants; so the thought is to create an abstract factory for the type and then concrete implementations for each variants that are then configured according to the need.

## Solution
The first thing to do in an Abstract factory pattern is to explicitly declare interfaces for the distinct types; then create implementations for each variant of the type.
the next move is to declare an abstract factory; an interface with a list of creation methods for all the products. these methods should be abstract and having the abstract type for a return type.
finally, for each variant, a factory implementation is created for each variant from the abstract factory.
the client code simply calls the factory variant it needs
## Structure
![[abstract_factory_structure.png]]
## Pseudo Code

```
// The abstract factory interface declares a set of methods that return different abstract products
// these product are called a family and are related by high-level theme or concept.
// products of one family are usually able to collaborate among themselves.
// a family of products may have several variants
interface GUIFactory is
    method createButton():Button
    method createCheckbox(): Checkbox

// concrete factories produce a family of products that belong to a single variant

class WinFactory implements GUIFactory is
    method createButton():Button is
        return new WinButton()
    method createCheckbox(): CheckBox is
        return new WinCheckbox()


// a different concrete factory
class MacFactory implements GUIFactory is method 
    createButton(): Button is
        return new MacButton()
    createCheckbox():Checkbox is 
        return new MacCheckbox()



// each distinct product should have a base interface, where all variants need to implement the interface
interface Button is 
    method paint()

interface Checkbox is
    method paint()

//concrete products are created for each factory
class WinButton implements Button is
    method paint() is
        // render a button in windows style

class WinCheckbox implements Checkbox is
    method paint() is 
        // render a checkbox in Windows style

class MacButton implements Button is 
    method paint() is
        // render a button in mac style

class MacCheckbox implements Checkbox is 
    method paint() is 
        // render a checkbox in mac style


// the client code works with factories and products through abstract types


class Application is 
    private field factory: GUIFactory
    private field button Button
    constructor(Application(factory: GUIFactory)) is
        this.factory = factory
    method createUI() is 
        this.button = factory.createButton()
    method paint() is
        button.paint()

// the application picks the factory type depending on the current configuration or environment settings and creates it at runtime
class ApplicationConfigurator is
    method main() is
        config = readApplicationConfigFile()
        if(config.OS == "Windows") then
            factory = new WinFactory()
        else if (config.OS == "Mac") then
            factory = new MacFactory()
        else
            throw new Exception("Error! Unknown operating system.")
        Application app = new Application(factory)
```

## When to use this pattern
- pretty self explanatory, when working with various families of related product, but you might need different variations for each product
- when handling different product variants and not wanting to worry about each creation process, this pattern instead allows the developer to just use interfaces instead without worrying about different types.
- when there is a set of factory methods that blur its primary responsibility
- each class should be responsible for one thing. when a class deals with multiple product types. it may be worth extracting its factory methods into a stand alone factory class of a full blown abstract factory implementation.

## Implementation notes
- map out a matrix of distinct product types versus variants
- declare abstract product interfaces, then create concrete product classes
- declare the abstract factory interface with a set of creation methods
- implement the concrete factory classes, one for each variant
- create factory init code somewhere, it should chose which variant depending on the environment configuration. then this factory object should be passed to all classes that need the products.
- scan through the code and find direct calls to constructors and replace them with calls to the factory creation method

## Pros and cons
### Pros
- products from the factory are always going to be compatible
- tight coupling between products and client code is avoided
- [[Single Responsibility Principle]], the product creation is extracted to one place
- [[Open-closed Principle]], new variants of products can be introduced without breaking the existing client code.
### Cons
- the code will become more complicated, sometimes even more complicated than what it should be, since new classes and interfaces are introduced
## Relations with other patterns
- many designers will start by using the [[Factory Method Design Pattern]] since it's less complicated and then will evolve toward the abstract factory, [[Prototype Design Pattern]] or [[Builder Design Pattern]] which are more flexible but more complicated
- [[Builder Design Pattern]] focuses on constructing complex objects step by step. while the [[Abstract Factory Design Pattern]] focuses on creating families of related objects; the abstract factory returns the product immediately, while the [[Builder Design Pattern]] lets you run additional steps (configuration)
- [[Abstract Factory Design Pattern]] classes often based on a set of [[Factory Method Design Pattern]] but can also use [[Prototype Design Pattern]] to compose the methods on these classes
- [[Abstract Factory Design Pattern]] can serve as an alternative to the [[Facade Design Pattern]] when you only want to hide the way the subsystem objects are created from the client code.
- [[Abstract Factory Design Pattern]] can be used alongside the [[Bridge Design Pattern]], this pairing is useful when some abstractions defined by the [[Bridge Design Pattern]] can only work with specific implementations. in this case the [[Abstract Factory Design Pattern]] can encapsulate these relations and hide the complexity from the client code.
- [[Abstract Factory Design Pattern]], [[Builder Design Pattern]] and [[Prototype Design Pattern]] can all be implemented as [[Singleton design pattern]]