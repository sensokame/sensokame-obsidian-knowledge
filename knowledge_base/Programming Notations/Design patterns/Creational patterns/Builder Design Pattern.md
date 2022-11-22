# Builder Design Pattern
this is a creational design pattern that lets you construct complex objects step by step. the pattern allows you to produce different types and representations of an object using the same construction code.

## Problem
imagine a complex object that requires laborious, step by step initialization of many fields and nested objects. Such initialization code is usually buried inside a monstrous constructor with lots of parameters or even worse: scattered all over the client code.
one approach is to subclass the base class into all combinations possible, but eventually this will become impossible with the growing number of combinations.
another approach would be to create one giant constructor with all the possible parameters. while this reduces the sub classing problem, it creates a new problem where most parameters would be unused and constructor calls would look very ugly.

## Solution
the builder pattern suggests that you can extract the object construction code out of its own class and move it to separate objects called builders.
![[house_builder_example.png]]
the pattern organized object construction into a set of steps, to create an object, the developer executes a series of the steps on a builder object. this way, not all the steps need to be called, but only the necessary ones for producing the needed configuration.
this can be combined with building different builder classes for different product variants.
### director
an extra step can be done by extracting a series of calls into a separate class called director, this director defines the order in which to execute the building steps while the builder provides the implementation.
a director isn't necessary, but it might be a good idea to put reusable routines.
additionally, this director class will hide the details of the product construction from the client code.

## Structure
![[builder_pattern_structure.png]]
## Pseudo Code

```
// Using the builder pattern makes sense only when your products are quite complex
class Car is
    // A car can have a GPS, trip computer, etc, different models of cars might have different features

class Manual is
    // Each car should have a user manual that corresponds to the car's configuration

// the builder interface specifies methods for creating the differnet parts of the product objects
interface Builder is
    method reset()
    method setSeats()
    method setEngine()
    method setTripComputer()
    method setGPS()

// The concrete builder classes follow the builder interface and provide specific implementations.
class CarBuilder implements Builder is 
    private field car: Car
    // A fresh builder instance should contain a blank product object
    constructor CarBuilder() is
        this.reset()
    // the reset method clears the object
    method reset() is
        this.car = new Car()
    // all production steps work with the same product instance.
    method setSeats() is
        // set number of seats
    method setEngine() is
        // install an engine
    method setTripComputer() is 
        // install a trip computer
    method setGPS() is
        // install a gps

    // concrete builders are supposed to provide their own methods for retrieving results. this is because each type of builder will create a different product that don't follow the same interface, so the result method can't be declared in the builder interface
    // usually after creating the product and returning it, the builder is ready to create a new product, that's why it's usual practice to reset the builder after returning the created object. however this isn't mandatory
    method getProduct(): Car is 
        product = this.car
        this.reset()
        return product

// unlike other creational patterns, builders let you construct products that don't follow the common interface
class CarManualBuilder implements Builder is
    private field manual: Manual

    constructor CarManualBuilder() is 
        this.reset()

    method reset() is
        this.manual = new Manual()
    method setSeats() is
        // document car seats features
    method setEngine() is
        // add engine instructions.
    method setTripComputer()
        // add trip computer instructions
    method setGPS() is
        // add gps instructions
    method getProduct(): Manual is
        // return manual and reset the builder

// the director is responsible for executing the building steps
// this is helpful when producing products according to a specific order or configuration
class Director is
    // the director works with any builder instance the client code passes to it. this way, the client code may alter the final type of the newly assembled product.
    method constructSportsCar(builder: Builder) is 
        builder.reset()
        builder.setSeats(2)
        builder.setEngine(new SportEnging())
        builder.setTripComputer(true)
        builder.setGPS(true)

    method constructSUV(builder: Builder) is 
    // same but for SUV


// the client code creates a builder object, passes it to the director and then initiates the construction process.
class Application is
    method makeCar() is
        Director director = new Director()
        CarBuilder builder = new CarBuilder()
        director.constructSportsCar(builder)
        Car car = builder.getProduct()
        CarManualBuilder builder = new CarManualBuilder()
        director.constructSportsCar(builder)
        Manual manual = builder.getProduct()
```

## When to use this pattern
- getting rid of telescoping constructor (which is creating a monster class with many overloaded constructors for the different configurations)
- creating different representations of some product
- constructing composite trees of other complex objects.

## Implementation notes
- define the common construction steps for building all available product representations.
- Declare the steps in the base builder interface
- create concrete builder class. don't forget to create the method that will fetch the construction result.
- consider creating a director class when needed.
- expose both the builder and director api to the client. let the client code build both objects before construction starts. the builder created by client will be passed to the director created by the client.
- the construction result can be obtained from the director only if all products follow the same interface. otherwise the client should fetch the result from the builder


## Pros and Cons
### Pros
- objects are constructed step by step
- the same construction code can be reused when building various representations
- [[Single Responsibility Principle]]. complex construction code can be isolated from the business logic
### Cons 
- the overall complexity will increase since the pattern requires creating multiple new classes
## Relation with other patterns
- many designers start with the [[Factory Method Design Pattern]] which is less complicated and evolve towards  [[Abstract Factory Design Pattern]], [[Prototype Design Pattern]] or [[Builder Design Pattern]] which are more flexible but more complicated
- [[Builder Design Pattern]] focuses on constructing complex objects step by step. while the [[Abstract Factory Design Pattern]] specialized in creating families of related objects, the abstract factory returns the product immediately whereas the [[Builder Design Pattern]] lets you run some additional construction steps before fetching the product.
- [[Builder Design Pattern]] can be used when creating complex [[Composite Design Pattern]] trees because you can program its construction steps to work recursively
- [[Builder Design Pattern]] can be combined when creating complex [[Bridge Design Pattern]]: the director class plays the role of the abstraction while different builders act as implementations
- [[Abstract Factory Design Pattern]], [[Builder Design Pattern]] and [[Prototype Design Pattern]] can all be implemented as singletons