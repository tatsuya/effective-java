# Chapter 7: Methods

## Item 38: Check parameters for validity

Each time you write a method or constructor, you should think about what restrictions exist on its parameters. You should document these restric- tions and enforce them with explicit checks at the beginning of the method body. It is important to get into the habit of doing this. The modest work that it entails will be paid back with interest the first time a validity check fails.

## Item 39: Make defensive copies when needed

If a class has mutable components that it gets from or returns to its clients, the class must defensively copy these components. If the cost of the copy would be prohibitive and the class trusts its clients not to modify the compo- nents inappropriately, then the defensive copy may be replaced by documentation outlining the client’s responsibility not to modify the affected components.

## Item 40: Design method signatures carefully

- Choose method names carefully. Names should always obey the standard naming conventions ([Item 56](chapter-8.md#item-56-adhere-to-generally-accepted-naming-conventions)).
- Don’t go overboard in providing convenience methods. Consider providing a “shorthand” only if it will be used often. When in doubt, leave it out.
- Avoid long parameter lists. Aim for four parameters or fewer.
- For parameter types, favor interfaces over classes ([Item 52](chapter-8.md#item-52-refer-to-objects-by-their-interfaces)).
- Prefer two-element enum types to boolean parameters.

## Item 41: Use overloading judiciously

Just because you can overload methods doesn’t mean you should. You should generally refrain from overloading methods with multiple signatures that have the same number of parameters. In some cases, especially where constructors are involved, it may be impossible to follow this advice. In that case, you should at least avoid situations where the same set of parameters can be passed to different overloadings by the addition of casts. If such a situation cannot be avoided, for example, because you are retrofitting an existing class to implement a new interface, you should ensure that all overloadings behave identically when passed the same parameters. If you fail to do this, programmers will be hard pressed to make effective use of the overloaded method or constructor, and they won’t understand why it doesn’t work.

## Item 42: Use varargs judiciously

Varargs methods are a convenient way to define methods that require a variable number of arguments, but they should not be overused. They can produce confusing results if used inappropriately.

## Item 43: Return empty arrays or collections, not nulls

There is no reason ever to return null from an array- or collection-valued method instead of returning an empty array or collection. The null-return idiom is likely a holdover from the C programming language, in which array lengths are returned separately from actual arrays. In C, there is no advantage to allocating an array if zero is returned as the length.

## Item 44: Write doc comments for all exposed API elements

Documentation comments are the best, most effective way to document your API. Their use should be considered mandatory for all exported API elements. Adopt a consistent style that adheres to standard conventions. Remember that arbitrary HTML is permissible within documentation comments and that HTML metacharacters must be escaped.