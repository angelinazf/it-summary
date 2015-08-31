struct是否使用指针的详细介绍 这里的class表示golang里面有指针的struct,struct表示golang里面没有指针的struct


Choosing Between Classes and Structures

You can use both classes and structures to define custom data types to use as the building blocks of your program’s code.

However, structure instances are always passed by value, and class instances are always passed by reference. This means that they are suited to different kinds of tasks. As you consider the data constructs and functionality that you need for a project, decide whether each data construct should be defined as a class or as a structure.

As a general guideline, consider creating a structure when one or more of these conditions apply:

The structure’s primary purpose is to encapsulate a few relatively simple data values.
It is reasonable to expect that the encapsulated values will be copied rather than referenced when you assign or pass around an instance of that structure.
Any properties stored by the structure are themselves value types, which would also be expected to be copied rather than referenced.
The structure does not need to inherit properties or behavior from another existing type.
Examples of good candidates for structures include:

The size of a geometric shape, perhaps encapsulating a width property and a height property, both of type Double.
A way to refer to ranges within a series, perhaps encapsulating a start property and a length property, both of type Int.
A point in a 3D coordinate system, perhaps encapsulating x, y and z properties, each of type Double.
In all other cases, define a class, and create instances of that class to be managed and passed by reference. In practice, this means that most custom data constructs should be classes, not structures.


#### 参考
https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-ID82