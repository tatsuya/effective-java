# Chapter 8: General Programming

This chapter is largely devoted to the nuts and bolts of the language. It discusses the treatment of local variables, control structures, the use of libraries, the use of various data types, and the use of two extralinguistic facilities: *reflection* and *native methods*. Finally, it discusses optimization and naming conventions.

## Item 45: Minimize the scope of local variables

- Declare a local variable where it is first used.
- Nealy every local variable declaration should contain an initializer, except `try-catch` statements.
- Prefer for loops to while loops.
- Keep methods small and focused.

