# Design Patterns;

> “Each pattern describes a problem which occurs over and over again in our
> environment, and then describes the core of the solution to that problem,
> in such a way that you can use this solution a million times over,
> without ever doing it the same way twice”
>
> Christopher Alexander

## GoF Patterns

> "Coding like poetry should be short and concise"
>
> Santosh Kalwar

### Creational Design Patterns

> "Any fool can write code that a computer can understand.
> Good programmers write code that humans can understand."
>
> Martin Fowler

#### Abstract Factory
Provides an interface for creating families of related or dependent objects
without specifying their concrete classes.

#### Builder
Separate the construction of a complex object from its representation
allowing the same construction process to create various representations.

#### Factory Method
Define an interface for creating an object, but lets subclasses decide which
class to instantiate.

#### Factory Method
Define an interface for creating an object, but lets subclasses decide which
class to instantiate.

#### Prototype
Specify the kinds of objects to create using a prototypical instance, and
create new objects by copying this prototype.

#### Singleton
Ensures a class has only one instance, and provides a global point of
access to it.

---

### Structural Design Patterns

> "Software and cathedrals are much the same –
> first we build them, then we pray."
>
> Samuel T. Redwine, Jr.

#### Adapter
Converts the interface of a class into another interface the clients expects.
Adapter lets classes work together that couldn’t otherwise because of
incompatible interfaces.

#### Bridge
The bridge design pattern is used to decouple the interfaces from
implementation and hiding the implementation details from the client program.

#### Composite
Used when we have to implement a part-whole hierarchy.
For example, a diagram made of other pieces such as circle, square,
triangle, etc.

#### Decorator
The decorator design pattern is used to modify the functionality of an
object at runtime.

#### Facade
Provides an unified interface to a set of interfaces in a subsystem.
Facade defines a higher-level interface that makes the subsystem easier to use.

#### Flyweight
Caching and reusing object instances, used with immutable objects.

#### Proxy
Provides a surrogate or placeholder for another object to controll access to it.

---

### Behavioral Design Patterns

> "I’m not a great programmer; I’m just a good programmer with great habits."
>
> Kent Beck


#### Chain Of Responsibility
Achieves loose coupling in software design where a request from
the client is passed to a chain of objects to process them.

#### Command
Encapsulates a request as an object, thereby letting you parameterize other
objects with different requests, queue or log requests, and support
undoable operations.

#### Iterator
Provides a way to access the elements of an aggregate object
sequentially without exposing its underlying representation.

#### Mediator
Provides a centralized communication medium between different objects
in a system.

#### Memento
When we want to save the state of an object so that we can restore later on.

#### Observer
Defines a one-to-many dependency between objects so that when one object
changes state, all it’s dependents are notified and updated automatically.

#### State
Allows an object to alter its behavior when its internal state changes.
The object will appear to change its class.

#### Strategy
Defines a family of algorithms encapsulates each one, and make them
interchangeable. Strategy lets the algorithm vary independetly from clients
that use it.

#### Template Method
Defines the skeleton of an algorithm in a method, deferring some steps to
subclasses. Template Method lets subclasses redefine certain steps of an
algorithm without changing the algorithm’s structure.

#### Chain Of Responsibility
Achieves loose coupling in software design where a request from
the client is passed to a chain of objects to process them.

---

## Resources

- https://refactoring.guru/
- https://martinfowler.com/eaaCatalog/
- https://www.amazon.com.br/Design-Patterns-Object-Oriented-Addison-Wesley-Professional-ebook/dp/B000SEIBB8
- https://www.amazon.com.br/Head-First-Design-Patterns-Freeman/dp/0596007124
