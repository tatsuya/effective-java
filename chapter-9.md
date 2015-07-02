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

- `IllegalArgumentException`: Non-null parameter value is inappropriate
- `IllegalStateException`: Object state is inappropriate for method invocation
- `NullPointerException`: Parameter value is null where prohibited
- `IndexOutOfBoundsException`: Index parameter value is out of range
- `ConcurrentModificationException`: Concurrent modification of an object has been detected where it is prohibited
- `UnsupportedOperationException`: Object does not support method
