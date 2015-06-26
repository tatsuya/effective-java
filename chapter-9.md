# Chapter 9: Exceptions

## Item 57: Use exceptions only for exceptional conditions

Exceptions are designed for use in exceptional conditions. Don’t use them for ordinary control flow, and don’t write APIs that force others to do so.

## Item 58: Use checked exceptions for recoverable conditions and runtime exceptions for programming errors

Use checked exceptions for recoverable conditions and runtime exceptions for programming errors. Of course, the situation is not always black and white. For example, consider the case of resource exhaustion, which can be caused by a programming error such as allocating an unreasonably large array or by a genuine shortage of resources. If resource exhaustion is caused by a temporary shortage or by temporarily heightened demand, the condition may well be recoverable. It is a matter of judgment on the part of the API designer whether a given instance of resource exhaustion is likely to allow for recovery. If you believe a condition is likely to allow for recovery, use a checked exception; if not, use a runtime exception. If it isn’t clear whether recovery is possible, you’re probably better off using an unchecked exception.