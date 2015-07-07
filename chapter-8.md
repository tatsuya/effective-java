# Chapter 8: General Programming

This chapter is largely devoted to the nuts and bolts of the language. It discusses the treatment of local variables, control structures, the use of libraries, the use of various data types, and the use of two extralinguistic facilities: *reflection* and *native methods*. Finally, it discusses optimization and naming conventions.

## Item 45: Minimize the scope of local variables

- Declare a local variable where it is first used.
- Nealy every local variable declaration should contain an initializer, except `try-catch` statements.
- Prefer for loops to while loops.
- Keep methods small and focused.

## Item 46: Prefer for-each loops to traditional for loops

The for-each loop provides compelling advantages over the traditional `for` loop in clarity and bug prevention, with no performance penalty. You should use it wherever you can. Unfortunately, there are three common situations where you can’t use a for-each loop:

1. **Filtering** — If you need to traverse a collection and remove selected elements, then you need to use an explicit iterator so that you can call its remove method.
2. **Transforming** — If you need to traverse a list or array and replace some or all of the values of its elements, then you need the list iterator or array index in order to set the value of an element.
3. **Parallel iteration** — If you need to traverse multiple collections in parallel, then you need explicit control over the iterator or index variable, so that all iterators or index variables can be advanced in lockstep.

## Item 47: Know and use the libraries

Don’t reinvent the wheel. By using a standard library, you take advantage of the knowledge of the experts who wrote it and the experience of those who used it before you.

## Item 48: Avoid float and double if exact answers are required

Don’t use float or double for any calculations that require an exact answer. Use `BigDecimal` if you want the system to keep track of the decimal point and you don’t mind the inconvenience and cost of not using a primitive type. Using `BigDecimal` has the added advantage that it gives you full control over rounding, letting you select from eight rounding modes whenever an operation that entails rounding is performed. This comes in handy if you’re performing business calculations with legally mandated rounding behavior. If performance is of the essence, you don’t mind keeping track of the decimal point yourself, and the quantities aren’t too big, use `int` or `long`. If the quantities don’t exceed nine decimal digits, you can use `int`; if they don’t exceed eighteen digits, you can use `long`. If the quantities might exceed eighteen digits, you must use `BigDecimal`.

## Item 49: Prefer primitive types to boxed primitives

Use primitives in preference to boxed primitives whenever you have the choice. Primitive types are simpler and faster. If you must use boxed primitives, be careful! Autoboxing reduces the verbosity, but not the danger, of using boxed primitives. When your program compares two boxed primitives with the == operator, it does an identity comparison, which is almost certainly not what you want. When your program does mixed-type computations involving boxed and unboxed primitives, it does unboxing, and when your program does unboxing, it can throw a NullPointerException. Finally, when your program boxes primitive values, it can result in costly and unnecessary object creations.

## Item 50: Avoid strings where other types are more appropriate

Avoid the natural tendency to represent objects as strings when better data types exist or can be written. Used inappropriately, strings are more cumbersome, less flexible, slower, and more error-prone than other types. Types for which strings are commonly misused include primitive types, enums, and aggregate types.

## Item 51: Beware the performance of string concatenation

Don’t use the string concatenation operator to combine more than a few strings unless performance is irrelevant. Use `StringBuilder`’s append method instead. Alternatively, use a character array, or process the strings one at a time instead of combining them.

## Item 52: Refer to objects by their interfaces

[Item 40](chapter-7.md#item-40-design-method-signatures-carefully) contains the advice that you should use interfaces rather than classes as parameter types. More generally, you should favor the use of interfaces rather than classes to refer to objects. If appropriate interface types exist, then parameters, return values, variables, and fields should all be declared using interface types. If you get into the habit of using interfaces as types, your program will be much more flexible.

## Item 53: Prefer interfaces to reflection

Reflection is a powerful facility that is required for certain sophisticated system programming tasks, but it has many disadvantages. If you are writing a program that has to work with classes unknown at compile time, you should, if at all possible, use reflection only to instantiate objects, and access the objects using some interface or superclass that is known at compile time.

## Item 54: Use native methods judiciously

Think twice before using native methods. Rarely, if ever, use them for improved performance. If you must use native methods to access low-level resources or legacy libraries, use as little native code as possible and test it thoroughly. A single bug in the native code can corrupt your entire application.

## Item 55: Optimize judiciously

Do not strive to write fast programs—strive to write good ones; speed will follow. Do think about performance issues while you’re designing systems and especially while you’re designing APIs, wire-level protocols, and persistent data formats. When you’ve finished building the system, measure its performance. If it’s fast enough, you’re done. If not, locate the source of the problems with the aid of a profiler, and go to work optimizing the relevant parts of the system. The first step is to examine your choice of algorithms: no amount of low-level optimization can make up for a poor choice of algorithm. Repeat this process as necessary, measuring the performance after every change, until you’re satisfied.

## Item 56: Adhere to generally accepted naming conventions

Internalize the standard naming conventions and learn to use them as second nature.
