# Chapter 3: Methods Common to All Objects

## Item 8: Obey the general contract when overriding equals

Here’s a recipe for a high-quality equals method:

- Use the `==` operator to check if the argument is a reference to this object. If so, return `true`.
- Use the `instanceof` operator to check if the argument has the correct type. If not, return `false`.
- Cast the argument to the correct type. Because this cast was preceded by an `instanceof` test, it is guaranteed to succeed.
- For each “significant” field in the class, check if that field of the argument matches the corresponding field of this object. If all these tests succeed, return `true`; otherwise, return `false`.
- When you are finished writing your `equals` method, ask yourself three questions: Is it symmetric? Is it transitive? Is it consistent?
- Always override hashCode when you override equals (Item 9).
- Don’t try to be too clever.
- Don’t substitute another type for `Object` in the `equals` declaration.

## Item 9: Always override hashCode when you override equals

You must override `hashCode` in every class that overrides `equals`. Failure to do so will result in a violation of the general contract for `Object.hashCode`, which will prevent your class from functioning properly in conjunction with all hash-based collections, including `HashMap`, `HashSet`, and `Hashtable`.

## Item 10: Always override toString

Whether or not you specify the format, provide programmatic access to all of the information contained in the value returned by `toString`.If you fail to do this, you force programmers who need this information to parse the string. Besides reducing performance and making unnecessary work for programmers, this process is error-prone and results in fragile systems that break if you change the format. By failing to provide accessors, you turn the string format into a de facto API, even if you’ve specified that it’s subject to change.

## Item 11: Override clone judiciously

All classes that implement `Cloneable` should override `clone` with a public method whose return type is the class itself. This method should first call `super.clone` and then fix any fields that need to be fixed. Typically, this means copying any mutable objects that comprise the internal “deep structure” of the object being cloned, and replacing the clone’s references to these objects with references to the copies. While these internal copies can generally be made by calling `clone` recursively, this is not always the best approach. If the class contains only primitive fields or references to immutable objects, then it is probably the case that no fields need to be fixed. There are exceptions to this rule. For example, a field representing a serial number or other unique ID or a field representing the object’s creation time will need to be fixed, even if it is primitive or immutable.
