# Chapter 11: Serialization

## Item 74: Implement Serializable judiciously

The ease of implementing Serializable is specious. Unless a class is to be thrown away after a short period of use, implementing Serializ- able is a serious commitment that should be made with care. Extra caution is warranted if a class is designed for inheritance. For such classes, an intermediate design point between implementing Serializable and prohibiting it in sub- classes is to provide an accessible parameterless constructor. This design point permits, but does not require, subclasses to implement Serializable.

## Item 75: Consider using a custom serialized form

When you have decided that a class should be serializable ([Item 74](chapter-11.md#item-74-implement-serializable-judiciously)), think hard about what the serialized form should be. Use the default serialized form only if it is a reasonable description of the logical state of the object; otherwise design a custom serialized form that aptly describes the object. You should allocate as much time to designing the serialized form of a class as you allocate to designing its exported methods ([Item 40](chapter-7.md#item-40-design-method-signatures-carefully)). Just as you cannot eliminate exported methods from future versions, you cannot eliminate fields from the serialized form; they must be preserved forever to ensure serialization compatibility. Choosing the wrong serialized form can have a permanent, negative impact on the complexity and performance of a class.
