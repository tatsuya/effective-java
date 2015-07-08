# Chapter 4: Classes and Interfaces

Classes and interfaces lie at the heart of the Java programming language. They are its basic units of abstraction. The language provides many powerful elements that you can use to design classes and interfaces. This chapter contains guidelines to help you make the best use of these elements so that your classes and interfaces are usable, robust, and flexible.

## Item 13: Minimize the accessibility of classes and members

*Information hiding* or *encapsulation*, is one of the fundamental tenets of software design. You should always reduce accessibility as much as possible. After carefully designing a minimal public API, you should prevent any stray classes, interfaces, or members from becoming a part of the API. With the exception of public static final fields, public classes should have no public fields. Ensure that objects referenced by public static final fields are immutable ([Item 15](chapter-4.md#item-15-minimize-mutability)).

## Item 14: In public classes, use accessor methods, not public fields

Public classes should never expose mutable fields. It is less harmful, though still questionable, for public classes to expose immutable fields. It is, however, sometimes desirable for package-private or private nested classes to expose fields, whether mutable or immutable, because this approach generates less visual clutter than the accessor-method approach, both in the class definition and in the client code that uses it.

## Item 15: Minimize mutability

An immutable class is simply a class whose instances cannot be modified. All of the information contained in each instance is provided when it is created and is fixed for the lifetime of the object. There are many good reasons for this: Immutable classes are easier to design, implement, and use than mutable classes. They are less prone to error and are more secure.

1. Don’t provide any methods that modify the object’s state (known as mutators).
2. Ensure that the class can’t be extended.
3. Make all fields final.
4. Make all fields private.
5. Ensure exclusive access to any mutable components.

## Item 16: Favor composition over inheritance

Inheritance is powerful, but it is problematic because it violates encapsulation. It is appropriate only when a genuine subtype relationship exists between the subclass and the superclass. Even then, inheritance may lead to fragility if the subclass is in a different package from the superclass and the superclass is not designed for inheritance. To avoid this fragility, use composition and forwarding instead of inheritance, especially if an appropriate interface to implement a wrapper class exists. Not only are wrapper classes more robust than subclasses, they are also more powerful.

## Item 17: Design and document for inheritance or else prohibit it

- The class must document precisely the effects of overriding any method.
- Constructors must not invoke overridable methods, directly or indirectly.
- If you implement Cloneable or Serializable in a class designed for inheritance, you should be aware that because the clone and readObject methods behave a lot like constructors.
- Prohibit subclassing in classes that are not designed and documented to be safely subclassed.

## Item 18: Prefer interfaces to abstract classes

The Java programming language provides two mechanisms for defining a type that permits multiple implementations: interfaces and abstract classes. The most obvious difference between the two mechanisms is that abstract classes are permitted to contain implementations for some methods while interfaces are not. A more important difference is that to implement the type defined by an abstract class, a class must be a subclass of the abstract class. Any class that defines all of the required methods and obeys the general contract is permitted to implement an interface, regardless of where the class resides in the class hierarchy. Because Java permits only single inheritance, this restriction on abstract classes severely constrains their use as type definitions.

While interfaces are not permitted to contain method implementations, using interfaces to define types does not prevent you from providing implementation assistance to programmers. You can combine the virtues of interfaces and abstract classes by providing an abstract *skeletal implementation* class to go with each nontrivial interface that you export. By convention, skeletal implementations are called AbstractInterface, where Interface is the name of the interface they implement. For example, the Collections Framework provides a skeletal implementation to go along with each main collection interface: AbstractCollection, AbstractSet, AbstractList, and AbstractMap.

## Item 19: Use interfaces only to define types

Interfaces should be used only to define types. They should not be used to export constants.

## Item 20: Prefer class hierarchies to tagged classes

Tagged classes are seldom appropriate. If you’re tempted to write a class with an explicit tag field, think about whether the tag could be eliminated and the class replaced by a hierarchy. When you encounter an existing class with a tag field, consider refactoring it into a hierarchy.

## Item 21: Use function objects to represent strategies

A primary use of function pointers is to implement the Strategy pattern. To implement this pattern in Java, declare an interface to represent the strategy, and a class that implements this interface for each concrete strategy. When a concrete strategy is used only once, it is typically declared and instantiated as an anonymous class. When a concrete strategy is designed for repeated use, it is generally implemented as a private static member class and exported in a public static final field whose type is the strategy interface.

## Item 22: Favor static member classes over nonstatic

There are four different kinds of nested classes, and each has its place. If a nested class needs to be visible outside of a single method or is too long to fit comfortably inside a method, use a member class. If each instance of the member class needs a reference to its enclosing instance, make it nonstatic; otherwise, make it static. Assuming the class belongs inside a method, if you need to create instances from only one location and there is a preexisting type that characterizes the class, make it an anonymous class; otherwise, make it a local class.
