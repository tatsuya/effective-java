# Chapter 9: Exceptions

## Item 57: Use exceptions only for exceptional conditions

Exceptions are designed for use in exceptional conditions. Don’t use them for ordinary control flow, and don’t write APIs that force others to do so.

## Item 58: Use checked exceptions for recoverable conditions and runtime exceptions for programming errors

Use checked exceptions for recoverable conditions and runtime exceptions for programming errors. Of course, the situation is not always black and white. For example, consider the case of resource exhaustion, which can be caused by a programming error such as allocating an unreasonably large array or by a genuine shortage of resources. If resource exhaustion is caused by a temporary shortage or by temporarily heightened demand, the condition may well be recoverable. It is a matter of judgment on the part of the API designer whether a given instance of resource exhaustion is likely to allow for recovery. If you believe a condition is likely to allow for recovery, use a checked exception; if not, use a runtime exception. If it isn’t clear whether recovery is possible, you’re probably better off using an unchecked exception.

## Item 59: Avoid unnecessary use of checked exceptions

As a litmus test, ask yourself how the programmer will handle the exception. Is this the best that can be done?

```java
} catch(TheCheckedException e) {
    throw new AssertionError(); // Can't happen!
}
```

How about this?

```java
} catch(TheCheckedException e) {
    e.printStackTrace();        // Oh well, we lose.
    System.exit(1);
}
```

If the programmer using the API can do no better, an unchecked exception would be more appropriate.

One technique for turning a checked exception into an unchecked exception is to break the method that throws the exception into two methods, the first of which returns a boolean that indicates whether the exception would be thrown. This API refactoring transforms the calling sequence from this:

```java
// Invocation with checked exception
try {
    obj.action(args);
} catch(TheCheckedException e) {
    // Handle exceptional condition
    ...
}
```

to this:

```java
// Invocation with state-testing method and unchecked exception
if (obj.actionPermitted(args)) {
    obj.action(args);
} else {
    // Handle exceptional condition
    ...
}
```

This refactoring is not always appropriate, but where it is appropriate, it can make an API more pleasant to use. While the latter calling sequence is no prettier than the former, the resulting API is more flexible. In cases where the programmer knows the call will succeed or is content to let the thread terminate if the call fails, the refactoring also allows this simple calling sequence:

```java
obj.action(args);
```

If you suspect that the simple calling sequence will be the norm, then this API refactoring may be appropriate.

## Item 60: Favor the use of standard exceptions

This list summarizes the most commonly reused exceptions:

- `IllegalArgumentException`: Non-null parameter value is inappropriate.
- `IllegalStateException`: Object state is inappropriate for method invocation. For example, this would be the exception to throw if the caller attempted to use some object before it has been properly initialized.
- `NullPointerException`: Parameter value is null where prohibited.
- `IndexOutOfBoundsException`: Index parameter value is out of range.
- `ConcurrentModificationException`: Concurrent modification of an object has been detected where it is prohibited.
- `UnsupportedOperationException`: Object does not support method.

Arguably, all erroneous method invocations boil down to an illegal argument or illegal state, but other exceptions are standardly used for certain kinds of illegal arguments and states. If a caller passes `null` in some parameter for which `null` values are prohibited, convention dictates that `NullPointerException` be thrown rather than `IllegalArgumentException`. Similarly, if a caller passes an out-of-range value in a parameter representing an index into a sequence, `IndexOutOfBoundsException` should be thrown rather than `IllegalArgumentException`.

## Item 61: Throw exceptions appropriate to the abstraction

If it isn’t feasible to prevent or to handle exceptions from lower layers, use exception translation, unless the lower-level method happens to guarantee that all of its exceptions are appropriate to the higher level. Chaining provides the best of both worlds: it allows you to throw an appropriate higher-level exception, while capturing the underlying cause for failure analysis (Item 63).

## Item 62: Document all exceptions thrown by each method

Document every exception that can be thrown by each method that you write. This is true for unchecked as well as checked exceptions, and for abstract as well as concrete methods. Provide individual `throws` clauses for each checked exception and do not provide `throws` clauses for unchecked exceptions. If you fail to document the exceptions that your methods can throw, it will be difficult or impossible for others to make effective use of your classes and interfaces.

## Item 63: Include failure-capture information in detail messages

It is critically important that the exception’s toString method return as much information as possible concerning the cause of the failure. In other words, the detail message of an exception should capture the failure for subsequent analysis.

## Item 64: Strive for failure atomicity

After an object throws an exception, it is generally desirable that the object still be in a well-defined, usable state, even if the failure occurred in the midst of performing an operation. This is especially true for checked exceptions, from which the caller is expected to recover. Generally speaking, a failed method invocation should leave the object in the state that it was in prior to the invocation. A method with this property is said to be failure atomic.

## Item 65: Don’t ignore exceptions

It is easy to ignore exceptions by surrounding a method invocation with a `try` statement with an empty `catch` block:

```java
// Empty catch block ignores exception - Highly suspect!
try {
    ...
} catch (SomeException e) {
}
```

An empty catch block defeats the purpose of exceptions, which is to force you to handle exceptional conditions. At the very least, the catch block should contain a comment explaining why it is appropriate to ignore the exception.
