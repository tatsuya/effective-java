# Chapter 2: Creating and Destroying Objects

This chapter concerns creating and destroying objects: when and how to create them, when and how to avoid creating them, how to ensure they are destroyed in a timely manner, and how to manage any cleanup actions that must precede their destruction.

## Item 1: Consider static factory methods instead of constructors

One advantage of static factory methods is that, unlike constructors, they have names.

```java
BigInteger(int, int, Random)
BigInteger.probablePrime     // Better expressed
```

A second advantage of static factory methods is that, unlike constructors, they are not required to create a new object each time they’re invoked.

```java
public static Boolean valueOf(boolean b) {
    return b ? Boolean.TRUE : Boolean.FALSE;
}
```

A third advantage of static factory methods is that, unlike constructors, they can return an object of any subtype of their return type.

For example, the class `java.util.EnumSet`, introduced in release 1.5, has no public constructors, only static factories. They return one of two implementations, depending on the size of the underlying enum type: if it has sixty-four or fewer elements, as most enum types do, the static factories return a `RegularEnumSet` instance, which is backed by a single `long`; if the enum type has sixty-five or more elements, the factories return a `JumboEnumSet` instance, backed by a `long` array.

A fourth advantage of static factory methods is that they reduce the verbosity of creating parameterized type instances.

```
Map<String, List<String>> m = new HashMap<String, List<String>>();
Map<String, List<String>> m = HashMap.newInstance();
```

The main disadvantage of providing only static factory methods is that classes without public or protected constructors cannot be subclassed.

A second disadvantage of static factory methods is that they are not readily distinguishable from other static methods.

Here are some common names for static factory methods:

- `valueOf` - Returns an instance that has, loosely speaking, the same value as its parameters. Such static factories are effectively type-conversion methods.
- `of` - A concise alternative to `valueOf`, popularized by `EnumSet` (Item 32).
- `getInstance` - Returns an instance that is described by the parameters but cannot be said to have the same value. In the case of a singleton, `getInstance` takes no parameters and returns the sole instance.
- `newInstance` - Like `getInstance`, except that newInstance guarantees that each instance returned is distinct from all others.
- `get`*Type*  - Like `getInstance`, but used when the factory method is in a different class. *Type* indicates the type of object returned by the factory method.
- `new`*Type* - Like `newInstance`, but used when the factory method is in a different class. *Type* indicates the type of object returned by the factory method.

In summary, static factory methods and public constructors both have their uses, and it pays to understand their relative merits. Often static factories are pref- erable, so avoid the reflex to provide public constructors without first considering static factories.

## Item 2: Consider a builder when faced with many constructor parameters

- Telescoping constructor pattern - does not scale well
- JavaBeans pattern - allows inconsistency, mandates mutability
- Builder pattern - is good when constructors or static factories would have more than a handful of parameters

```java
// Builder Pattern
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;

    public static class Builder {
        // Required parameters
        private final int servingSize;
        private final int servings;

        // Optional parameters - initialized to default values
        private int calories      = 0;
        private int fat           = 0;
        private int carbohydrate  = 0;
        private int sodium        = 0;

        public Builder(int servingSize, int servings) {
            this.servingSize = servingSize;
            this.servings    = servings;
        }

        public Builder calories(int val) {
            calories = val;
            return this;
        }

        public Builder fat(int val) {
            fat = val;
            return this;
        }

        public Builder carbohydrate(int val) {
            carbohydrate = val;
            return this;
        }

        public Builder sodium(int val) {
            sodium = val;
            return this;
        }

        public NutritionFacts build() {
            return new NutritionFacts(this);
        }
    }

    private NutritionFacts(Builder builder) {
        servingSize  = builder.servingSize;
        servings     = builder.servings;
        calories     = builder.calories;
        fat          = builder.fat;
        sodium       = builder.sodium;
        carbohydrate = builder.carbohydrate;
    }
}
```

Note that `NutritionFacts` is immutable, and that all parameter default values are in a single location. The builder’s setter methods return the builder itself so that invocations can be chained. Here’s how the client code looks:

```java
NutritionFacts cocaCola = new NutritionFacts.Builder(240, 8).
    calories(100).sodium(35).carbohydrate(27).build();
```

## Item 3: Enforce the singleton property with a private constructor or an enum type

A single-element enum type is the best way to implement a singleton.

```java
// Enum singleton - the preferred approach
public enum Elvis {
   INSTANCE;
   public void leaveTheBuilding() { ... }
}
```

## Item 4: Enforce noninstantiability with a private constructor

Attempting to enforce noninstantiability by making a class abstract does not work.

```java
// Noninstantiable utility class
public class UtilityClass {
    // Suppress default constructor for noninstantiability
    private UtilityClass() {
        throw new AssertionError();
    }
    ...  // Remainder omitted
}
```

The AssertionError isn’t strictly required, but it provides insurance in case the constructor is accidentally invoked from within the class.

## Item 5: Avoid creating unnecessary objects

```java
String s = new String("stringette"); // DON'T DO THIS!
String s = "stringette";
```

This version uses a single String instance, rather than creating a new one each time it is executed. Furthermore, it is guaranteed that the object will be reused by any other code running in the same virtual machine that happens to con- tain the same string literal.

This class models a person and has an `isBabyBoomer` method that tells whether the person is a "baby boomer," in other words, whether the person was born between 1946 and 1964:

```java
public class Person {
    private final Date birthDate;
    // Other fields, methods, and constructor omitted

    // DON'T DO THIS!
    public boolean isBabyBoomer() {
        // Unnecessary allocation of expensive object
        Calendar gmtCal =
            Calendar.getInstance(TimeZone.getTimeZone("GMT"));
        gmtCal.set(1946, Calendar.JANUARY, 1, 0, 0, 0);
        Date boomStart = gmtCal.getTime();
        gmtCal.set(1965, Calendar.JANUARY, 1, 0, 0, 0);
        Date boomEnd = gmtCal.getTime();
        return birthDate.compareTo(boomStart) >= 0 &&
               birthDate.compareTo(boomEnd)   <  0;
    }
}
```

The improved version of the `Person` class:

```java
class Person {
    private final Date birthDate;
    // Other fields, methods, and constructor omitted

    /**
    * The starting and ending dates of the baby boom.
    */
    private static final Date BOOM_START;
    private static final Date BOOM_END;
    static {
        Calendar gmtCal =
            Calendar.getInstance(TimeZone.getTimeZone("GMT"));
        gmtCal.set(1946, Calendar.JANUARY, 1, 0, 0, 0);
        BOOM_START = gmtCal.getTime();
        gmtCal.set(1965, Calendar.JANUARY, 1, 0, 0, 0);
        BOOM_END = gmtCal.getTime();
    }

   public boolean isBabyBoomer() {
       return birthDate.compareTo(BOOM_START) >= 0 &&
              birthDate.compareTo(BOOM_END)   <  0;
    }
}
```

Prefer primitives to boxed primitives, and watch out for unintentional autoboxing.

```java
// Slow
public static void main(String[] args) {
    Long sum = 0L;
    for (long i = 0; i < Integer.MAX_VALUE; i++) {
        sum += i;
    }
    System.out.println(sum);
}

// Faster
public static void main(String[] args) {
    long sum = 0L;
    for (long i = 0; i < Integer.MAX_VALUE; i++) {
        sum += i;
    }
    System.out.println(sum);
}
```

## Item 6: Eliminate obsolete object references

Nulling out object references should be the exception rather than the norm.

Whenever a class manages its own memory, the programmer should be alert for memory leaks.

Another common source of memory leaks is caches.

A third common source of memory leaks is listeners and other callbacks.

## Item 7: Avoid finalizers

Finalizers are unpredictable, often dangerous, and generally unnecessary.

- There is no guarantee they’ll be executed promptly
- It provides no guarantee that they’ll get executed at all
- If an uncaught exception is thrown during finalization, the exception is ignored, and finalization of that object terminates
- There is a severe performance penalty for using finalizers.

Instead, provide an explicit termination method, and require clients of the class to invoke this method on each instance when it is no longer needed. Explicit termination methods are typically used in combination with the try-finally construct to ensure termination.

```java
// try-finally block guarantees execution of termination method
Foo foo = new Foo(...);
try {
    // Do what must be done with foo
    ...
} finally {
    foo.terminate();  // Explicit termination method
}
```
