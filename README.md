# effective-java

Summarized version of Effective Java 2nd Edition.

## [Chapter 2: Creating and Destroying Objects](chapter-2.md)

- [Item 1: Consider static factory methods instead of constructors](chapter-2.md#item-1-consider-static-factory-methods-instead-of-constructors)
- [Item 2: Consider a builder when faced with many constructor parameters](chapter-2.md#item-2-consider-a-builder-when-faced-with-many-constructor-parameters)
- [Item 3: Enforce the singleton property with a private constructor or an enum type](chapter-2.md#item-3-enforce-the-singleton-property-with-a-private-constructor-or-an-enum-type)
- [Item 4: Enforce noninstantiability with a private constructor](chapter-2.md#item-4-enforce-noninstantiability-with-a-private-constructor)
- [Item 5: Avoid creating unnecessary objects](chapter-2.md#item-5-avoid-creating-unnecessary-objects)
- [Item 6: Eliminate obsolete object references](chapter-2.md#item-6-eliminate-obsolete-object-references)
- [Item 7: Avoid finalizers](chapter-2.md#item-7-avoid-finalizers)

## [Chapter 3: Methods Common to All Objects](chapter-3.md)

- [Item 8: Obey the general contract when overriding equals](chapter-3.md#item-8-obey-the-general-contract-when-overriding-equals)
- [Item 9: Always override hashCode when you override equals](chapter-3.md#item-9-always-override-hashcode-when-you-override-equals)
- [Item 10: Always override toString](chapter-3.md#item-10-always-override-tostring)
- [Item 11: Override clone judiciously](chapter-3.md#item-11-override-clone-judiciously)
- [Item 12: Consider implementing Comparable](chapter-3.md#item-12-consider-implementing-comparable)

## [Chapter 4: Classes and Interfaces](chapter-4.md)

- [Item 13: Minimize the accessibility of classes and members](chapter-4.md#item-13-minimize-the-accessibility-of-classes-and-members)
- [Item 14: In public classes, use accessor methods, not public fields](chapter-4.md#item-14-in-public-classes-use-accessor-methods-not-public-fields)
- [Item 15: Minimize mutability](chapter-4.md#item-15-minimize-mutability)
- [Item 16: Favor composition over inheritance](chapter-4.md#item-16-favor-composition-over-inheritance)
- [Item 17: Design and document for inheritance or else prohibit it](chapter-4.md#item-17-design-and-document-for-inheritance-or-else-prohibit-it)
- [Item 18: Prefer interfaces to abstract classes](chapter-4.md#item-18-prefer-interfaces-to-abstract-classes)
- [Item 19: Use interfaces only to define types](chapter-4.md#item-19-use-interfaces-only-to-define-types)
- [Item 20: Prefer class hierarchies to tagged classes](chapter-4.md#item-20-prefer-class-hierarchies-to-tagged-classes)
- [Item 21: Use function objects to represent strategies](chapter-4.md#item-21-use-function-objects-to-represent-strategies)
- [Item 22: Favor static member classes over nonstatic](chapter-4.md#item-22-favor-static-member-classes-over-nonstatic)

## [Chapter 5: Generics](chapter-5.md)

- [Item 23: Don’t use raw types in new code](chapter-5.md#item-23-don’t-use-raw-types-in-new-code)
- [Item 24: Eliminate unchecked warnings](chapter-5.md#item-24-eliminate-unchecked-warnings)
- [Item 25: Prefer lists to arrays](chapter-5.md#item-25-prefer-lists-to-arrays)
- [Item 26: Favor generic types](chapter-5.md#item-26-favor-generic-types)
- [Item 27: Favor generic methods](chapter-5.md#item-27-favor-generic-methods)
- [Item 28: Use bounded wildcards to increase API flexibility](chapter-5.md#item-28-use-bounded-wildcards-to-increase-api-flexibility)
- [Item 29: Consider type safe heterogeneous containers](chapter-5.md#item-29-consider-type-safe-heterogeneous-containers)

## [Chapter 6: Enums and Annotations](chapter-6.md)

- [Item 30: Use enums instead of int constants](chapter-6.md#item-30-use-enums-instead-of-int-constants)
- [Item 31: Use instance fields instead of ordinals](chapter-6.md#item-31-use-instance-fields-instead-of-ordinals)
- [Item 32: Use EnumSet instead of bit fields](chapter-6.md#item-32-use-enumset-instead-of-bit-fields)
- [Item 33: Use EnumMap instead of ordinal indexing](chapter-6.md#item-33-use-enummap-instead-of-ordinal-indexing)
- [Item 34: Emulate extensible enums with interfaces](chapter-6.md#item-34-emulate-extensible-enums-with-interfaces)
- [Item 35: Prefer annotations to naming patterns](chapter-6.md#item-35-prefer-annotations-to-naming-patterns)
- [Item 36: Consistently use the Override annotation](chapter-6.md#item-36-consistently-use-the-override-annotation)
- [Item 37: Use marker interfaces to define types](chapter-6.md#item-37-use-marker-interfaces-to-define-types)

## [Chapter 7: Methods](chapter-7.md)

- [Item 38: Check parameters for validity](chapter-7.md#item-38-check-parameters-for-validity)
- [Item 39: Make defensive copies when needed](chapter-7.md#item-39-make-defensive-copies-when-needed)
- [Item 40: Design method signatures carefully](chapter-7.md#item-40-design-method-signatures-carefully)
- [Item 41: Use overloading judiciously](chapter-7.md#item-41-use-overloading-judiciously)
- [Item 42: Use varargs judiciously](chapter-7.md#item-42-use-varargs-judiciously)
- [Item 43: Return empty arrays or collections, not nulls](chapter-7.md#item-43-return-empty-arrays-or-collections-not-nulls)
- [Item 44: Write doc comments for all exposed API elements](chapter-7.md#item-44-write-doc-comments-for-all-exposed-api-elements)

## [Chapter 8: General Programming](chapter-8.md)

- [Item 45: Minimize the scope of local variables](chapter-8.md#item-45-minimize-the-scope-of-local-variables)
- [Item 46: Prefer for-each loops to traditional for loops](chapter-8.md#item-46-prefer-for-each-loops-to-traditional-for-loops)
- [Item 47: Know and use the libraries](chapter-8.md#item-47-know-and-use-the-libraries)
- [Item 48: Avoid float and double if exact answers are required](chapter-8.md#item-48-avoid-float-and-double-if-exact-answers-are-required)
- [Item 49: Prefer primitive types to boxed primitives](chapter-8.md#item-49-prefer-primitive-types-to-boxed-primitives)
- [Item 50: Avoid strings where other types are more appropriate](chapter-8.md#item-50-avoid-strings-where-other-types-are-more-appropriate)
- [Item 51: Beware the performance of string concatenation](chapter-8.md#item-51-beware-the-performance-of-string-concatenation)
- [Item 52: Refer to objects by their interfaces](chapter-8.md#item-52-refer-to-objects-by-their-interfaces)
- [Item 53: Prefer interfaces to reflection](chapter-8.md#item-53-prefer-interfaces-to-reflection)
- [Item 54: Use native methods judiciously](chapter-8.md#item-54-use-native-methods-judiciously)
- [Item 55: Optimize judiciously](chapter-8.md#item-55-optimize-judiciously)
- [Item 56: Adhere to generally accepted naming conventions](chapter-8.md#item-56-adhere-to-generally-accepted-naming-conventions)

## [Chapter 9: Exceptions](chapter-9.md)

- [Item 57: Use exceptions only for exceptional conditions](chapter-9.md#item-57-use-exceptions-only-for-exceptional-conditions)
- [Item 58: Use checked exceptions for recoverable conditions and runtime exceptions for programming errors](chapter-9.md#item-58-use-checked-exceptions-for-recoverable-conditions-and-runtime-exceptions-for-programming-errors)
- [Item 59: Avoid unnecessary use of checked exceptions](chapter-9.md#item-59-avoid-unnecessary-use-of-checked-exceptions)
- [Item 60: Favor the use of standard exceptions](chapter-9.md#item-60-favor-the-use-of-standard-exceptions)
- [Item 61: Throw exceptions appropriate to the abstraction](chapter-9.md#item-61-throw-exceptions-appropriate-to-the-abstraction)
- [Item 62: Document all exceptions thrown by each method](chapter-9.md#item-62-document-all-exceptions-thrown-by-each-method)
- [Item 63: Include failure-capture information in detail messages](chapter-9.md#item-63-include-failure-capture-information-in-detail-messages)
- [Item 64: Strive for failure atomicity](chapter-9.md#item-64-strive-for-failure-atomicity)
- [Item 65: Don’t ignore exceptions](chapter-9.md#item-65-don’t-ignore-exceptions)

## [Chapter 10: Concurrency](chapter-10.md)

- [Item 66: Synchronize access to shared mutable data](chapter-10.md#item-66-synchronize-access-to-shared-mutable-data)
- [Item 67: Avoid excessive synchronization](chapter-10.md#item-67-avoid-excessive-synchronization)
- [Item 68: Prefer executors and tasks to threads](chapter-10.md#item-68-prefer-executors-and-tasks-to-threads)
- [Item 69: Prefer concurrency utilities to wait and notify](chapter-10.md#item-69-prefer-concurrency-utilities-to-wait-and-notify)
- [Item 70: Document thread safety](chapter-10.md#item-70-document-thread-safety)
- [Item 71: Use lazy initialization judiciously](chapter-10.md#item-71-use-lazy-initialization-judiciously)
- [Item 72: Don’t depend on the thread scheduler](chapter-10.md#item-72-don’t-depend-on-the-thread-scheduler)
- [Item 73: Avoid thread groups](chapter-10.md#item-73-avoid-thread-groups)

## [Chapter 11: Serialization](chapter-11.md)

- [Item 74: Implement Serializable judiciously](chapter-11.md#item-74-implement-serializable-judiciously)
- [Item 75: Consider using a custom serialized form](chapter-11.md#item-75-consider-using-a-custom-serialized-form)
- [Item 76: Write readObject methods defensively](chapter-11.md#item-76-write-readobject-methods-defensively)
- [Item 77: For instance control, prefer enum types to readResolve](chapter-11.md#item-77-for-instance-control-prefer-enum-types-to-readresolve)
- [Item 78: Consider serialization proxies instead of serialized instances](chapter-11.md#item-78-consider-serialization-proxies-instead-of-serialized-instances)
