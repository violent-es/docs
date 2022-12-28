# Comparison to Other Languages

## String type

VioletScript supports an UTF-8 encoded string type. Most of the methods exposed by `String` type use Code Point indexes, which can be inefficient in large strings. For faster access, there are few UTF-8 specific methods that are efficient regardless of string length, and manipulable iterators (`stringValue.iterate` and `stringValue.iterateRightToLeft`).

More information on `String` type: [String Type](./types/string.md)