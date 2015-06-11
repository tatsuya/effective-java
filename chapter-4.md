# Chapter 4: Classes and Interfaces

## Item 13: Minimize the accessibility of classes and members

- This concept, known as information hiding or encapsulation, is one of the fundamental tenets of software design.
- Make each class or member as inaccessible as possible.

## Item 14: In public classes, use accessor methods, not public fields

Public classes should never expose mutable fields. It is less harmful, though still questionable, for public classes to expose immutable fields. It is, however, sometimes desirable for package-private or private nested classes to expose fields, whether mutable or immutable.

## Item 15: Minimize mutability

An immutable class is simply a class whose instances cannot be modified. All of the information contained in each instance is provided when it is created and is fixed for the lifetime of the object. There are many good reasons for this: Immutable classes are easier to design, implement, and use than mutable classes. They are less prone to error and are more secure.

1. Don’t provide any methods that modify the object’s state (known as mutators).
2. Ensure that the class can’t be extended.
3. Make all fields final.
4. Make all fields private.
5. Ensure exclusive access to any mutable components.
