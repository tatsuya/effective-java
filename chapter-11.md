# Chapter 11: Serialization

## Item 74: Implement Serializable judiciously

The ease of implementing Serializable is specious. Unless a class is to be thrown away after a short period of use, implementing Serializ- able is a serious commitment that should be made with care. Extra caution is war- ranted if a class is designed for inheritance. For such classes, an intermediate design point between implementing Serializable and prohibiting it in sub- classes is to provide an accessible parameterless constructor. This design point permits, but does not require, subclasses to implement Serializable.