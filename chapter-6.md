# Chapter 6: Enums and Annotations

## Item 30: Use enums instead of int constants

The advantages of enum types over int constants are compelling. Enums are far more readable, safer, and more powerful. Many enums require no explicit constructors or members, but many others benefit from associating data with each constant and providing methods whose behavior is affected by this data. Far fewer enums benefit from associating multiple behaviors with a single method. In this relatively rare case, prefer constant-specific methods to enums that switch on their own values. Consider the strategy enum pattern if multiple enum constants share common behaviors.

## Item 31: Use instance fields instead of ordinals

Most programmers will have no use for this method. It is designed for use by general-purpose enum-based data structures such as EnumSet and EnumMap. Unless you are writing such a data structure, you are best off avoiding the ordinal method entirely.
