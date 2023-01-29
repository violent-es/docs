# Comparison to Other Languages

## String type

VioletScript supports an UTF-8 encoded string type. Methods exposed by `String` type use Code Point indexes. Solely using `Int` for indexing can be inefficient in large strings. For faster access, use `StringIndex` objects for indexing. The built-in `UTF8` object also provides UTF-8 specific methods that are efficient regardless of string length. VioletScript also supports flexible iterators (`stringValue.chars` and `stringValue.rightToLeftChars`).

More information on `String` type: [String Type](./types/string.md)