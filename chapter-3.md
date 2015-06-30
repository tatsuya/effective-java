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
