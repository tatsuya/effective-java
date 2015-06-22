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
