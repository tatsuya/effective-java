# Chapter 3: Methods Common to All Objects

## Item 8: Obey the general contract when overriding equals

Here’s a recipe for a high-quality equals method:

- Use the `==` operator to check if the argument is a reference to this object. If so, return `true`.
- Use the `instanceof` operator to check if the argument has the correct type. If not, return `false`.
- Cast the argument to the correct type. Because this cast was preceded by an `instanceof` test, it is guaranteed to succeed.
- For each “significant” field in the class, check if that field of the argument matches the corresponding field of this object. If all these tests succeed, return `true`; otherwise, return `false`.
- When you are finished writing your `equals` method, ask yourself three questions: Is it symmetric? Is it transitive? Is it consistent?
- Always override `hashCode` when you override `equals` ([Item 9](chapter-3.md#item-9-always-override-hashcode-when-you-override-equals)).
- Don’t try to be too clever.
- Don’t substitute another type for `Object` in the `equals` declaration.

## Item 9: Always override hashCode when you override equals

You must override `hashCode` in every class that overrides `equals`. Failure to do so will result in a violation of the general contract for `Object.hashCode`, which will prevent your class from functioning properly in conjunction with all hash-based collections, including `HashMap`, `HashSet`, and `Hashtable`.

## Item 10: Always override toString

Whether or not you specify the format, provide programmatic access to all of the information contained in the value returned by `toString`. For example, the `PhoneNumber` class should contain accessors for the area code, prefix, and line number. If you fail to do this, you force programmers who need this information to parse the string. Besides reducing performance and making unnecessary work for programmers, this process is error-prone and results in fragile systems that break if you change the format. By failing to provide accessors, you turn the string format into a de facto API, even if you’ve specified that it’s subject to change.

## Item 11: Override clone judiciously

All classes that implement `Cloneable` should override `clone` with a public method whose return type is the class itself. This method should first call `super.clone` and then fix any fields that need to be fixed. Typically, this means copying any mutable objects that comprise the internal “deep structure” of the object being cloned, and replacing the clone’s references to these objects with references to the copies. While these internal copies can generally be made by calling `clone` recursively, this is not always the best approach. If the class contains only primitive fields or references to immutable objects, then it is probably the case that no fields need to be fixed. There are exceptions to this rule. For example, a field representing a serial number or other unique ID or a field representing the object’s creation time will need to be fixed, even if it is primitive or immutable.

## Item 12: Consider implementing Comparable

In the following description, the notation `sgn(expression)` designates the mathematical signum function, which is defined to return -1, 0, or 1, according to whether the value of expression is negative, zero, or positive.

- The implementor must ensure `sgn(x.compareTo(y)) == -sgn(y.compareTo(x))` for all `x` and `y`. (This implies that `x.compareTo(y)` must throw an exception if and only if `y.compareTo(x)` throws an exception.)
- The implementor must also ensure that the relation is transitive: `(x.compareTo(y) > 0 && y.compareTo(z) > 0)` implies `x.compareTo(z) > 0`.
- Finally, the implementor must ensure that `x.compareTo(y) == 0` implies that `sgn(x.compareTo(z)) == sgn(y.compareTo(z))`, for all `z`.
- It is strongly recommended, but not strictly required, that `(x.compareTo(y) == 0) == (x.equals(y))`. Generally speaking, any class that implements the `Comparable` interface and violates this condition should clearly indicate this fact. The recommended language is “Note: This class has a natural ordering that is inconsistent with equals.”
