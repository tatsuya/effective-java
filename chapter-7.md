# Chapter 7: Methods

## Item 38: Check parameters for validity

Each time you write a method or constructor, you should think about what restrictions exist on its parameters. You should document these restric- tions and enforce them with explicit checks at the beginning of the method body. It is important to get into the habit of doing this. The modest work that it entails will be paid back with interest the first time a validity check fails.