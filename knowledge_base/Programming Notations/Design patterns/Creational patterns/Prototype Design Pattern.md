# Prototype Design Pattern
Prototype is a design pattern that lets you copy existing objects without making your code dependent on their classes.
## Problem
the problem here is, say we want to create a copy of an existing object, the most direct approach is creating a new instance and then copying the fields; while this could be fast and direct it is a big problem, for it's a dirty copy, and most importantly, some fields are private and will not be copied alongside; plus, copying like this would make our new class dependent on the copied class. and sometimes, the current class only has visibility on the interface and not the actual members.
# Solution
The solution is quiet simple; delegate the copy creation to the actual object being cloned instead of the current class that needs a copy.
this is simply done by implementing a ``clone``  method in the class of the object being cloned, and call that method whenever it is needed.
>**NOTE:** in most modern programming language, a `Cloneable` interface is provided and whenever a class supports being cloned, it would implement this interface and the `Clone` method that comes with it to provide the prototype design pattern implementation

the object that supports being cloned is called a ``prototype``, and sometimes, when an object has too many fields and possible configuration, cloning would be a better alternative than sub classing.
>**NOTE:** this is fairly seen when a single prototype instance is being created for a specific configuration, and then when a new instance of that configuration is required, the prototype is cloned and then changed to suit the new needs.

## Structure
![[structure_prototype_design_pattern.png]]
usually, a registry is needed to create the cloned instances
![[structure_prototype_registry.png]]
# Pseudo Code
```pseudo
// Base Prototype.
abstract class Shape is
    field X: int
    field Y: int
    field color: string

    // a regular constructor.
    constructor Shape() is 
	    // ...
	// prototype constructor. a fresh object is initialized
	// with values from the existing object
	constructor Shape(source: Shape) is 
		this()
		this.X = source.X
		this.Y = source.Y
		this.color = source.color
	// the clone operation which will return oe fht shape subclasses.

// concrete prototype, the cloning method create a new object in one go
// by calling the constructor of the current class and passing the current
// object as a constructor argument.
// perform all the actual copying in the constructor to help keep the result
// consistent: the constructor will not return a result until the new object is fully build; this, no object can have a reference to a partially build clone.
class Rectangle extends Shape is
    field width: int
    field height:int
    constructor Rectangle(source: Rectangle) is
	    // a parent constructor call is needed to copy private fields
	    // defined in the parent class
	    super(source)
	    this.width = source.width
	    this.heigh = source.height
	method clone(): Shape is 
	    return new Rectangle(this)

class Circle extends Shape is
    field radius: int
    constructor Circle(source: Circle) is
	    super(source)
	    this.radius = source.radius
	method clone(): Shape is 
		return new Circle(this)


// somewhere in the client code.
class Application is 
	field shapes: array of shape
	constructor Application() is
		Circle circle = new Circle()
		circle.X = 10
		circle.Y = 10
		circle.radius = 20
		shapes.add(circle)

		circle anotherCircle = circle.clone()
		shapes.add(anotherCircle)
		// the `anotherCircle` variable contains an exact copy

		Rectangle rectangle = new Rectangle()
		rectangle.width = 10
		rectangle.height = 20
		shapes.add(rectangle)
	method businessLogic() is
		// prototype rocks because it  lets you produce a copy of an object
		// without knowing anything about its type
		Array shapesCopy = new Array of Shapes.

		// for instance we don't know the exact element in the shapes array
		// all we know is that they are all shapes
		// but since the base prototype class also has the clone method
		// we can call that clone method on all the objects regardless of their subclass
		// this is why we get proper clones instead of a set of simple shape objects
		foreach (s in shapes) do
			shapesCopy.add(s.clone)
		// the `shapesCopy` array contains exact copies of the ``shapes array children
```

## when to use this prototype
- Use this pattern when the code shouldn't depend on the concrete classes of the objects you need to copy.
> this happens a lot when using 3rd-party code via some interfaces.

- Use this pattern when you want to reduce the number of sub classes that only differ in initialization 
> this happens when having a complex class that requires a lot of configuration before being used. to reduce the duplication, we can create sub classes and put common configuration code into their constructors and the clone the configuration subclass  you need.

## Implementation notes
- if the programming language doesn't already have one, create a prototype interface and declare the ``method`` into it.
- define the alternative constructor that accepts an object of that class as an argument in the prototype class, the constructor must copy the values of all the fields defined in the class from the passed object. when changing a subclass, calling the parent constructor is a must to let the super class handle the cloning of the internal fields.
> In case the programming language doesn't support method overloading, a separate prototype constructor will not be possible to create, in that case, just clone the fields in the clone method itself. (this is not safe, but sometimes necessary)

- the cloning method usually consists of running just the new operator with the prototypical version of the constructor. 
- optional: create a centralized prototype registry to store a catalog of frequently used prototypes.
> the registry can be implemented as a factory class or put in the base prototype class with a static method for fetching the prototype.

## Pros and Cons
### Pro
- objects are clonable without coupling the concrete classes.
- repeated initialization can be discarded in favor of cloning pre-built prototypes
- complex object can be produced more conveniently
- prototype design pattern is an alternative to inheritance when dealing with configuration presets for complex objects
### Cons
- it is tricky to clone complex objects that have circular references
## Relations with other patterns
### [[Factory Method Design Pattern]]
- many designers start by using this [[Factory Method Design Pattern]] since it's less complicated and more customizable via subclasses, and then they evolve toward [[Abstract Factory Design pattern]], [[Prototype Design Pattern]] and [[Builder Design Pattern]] since they are more flexible but more complicated

- [[Factory Method Design Pattern]] is based on inheritance but doesn't require an initialization step, while [[Prototype Design Pattern]] is based on inheritance so it requires a complicated initialization

### [[Abstract Factory Design pattern]]
- classes are often based on a set of [[Factory Method Design Pattern]], but can also use [[Prototype Design Pattern]] to compose the methods on these classes

### [[Command Design Pattern]]
- Commands can be saved into history by the [[Prototype Design Pattern]]

### [[Composite Design Pattern]] and  [[Decorator Design Pattern]]
- designs that make heavy use of the [[Composite Design Pattern]] and [[Decorator Design Pattern]] can often benefit from using the [[Prototype Design Pattern]], applying the pattern lets you clone complex structures instead of constructing them from scratch

### [[Singleton design pattern]]
- [[Prototype Design Pattern]], [[Abstract Factory Design pattern]] and [[Builder Design Pattern]] can all be implemented as [[Singleton design pattern]]

### [[Memento Design Pattern]]
- [[Prototype Design Pattern]] can be a similar alternative to [[Memento Design Pattern]], this works if the object, the state of which you want to store in the history, is straightforward and doesn't have links to external resources, or the links are easy to re-establish.
## useful links
[refactoring guru prototype page](https://refactoring.guru/design-patterns/prototype)
