# Built-in objects

All of the built-in declarations listed here are defined in the top-level package, except if otherwise explicitly annotated. The programmer may explicitly use `global` if one of the built-in names conflict with personal program names.

Uncategorized:

- `Iterator.<T>` interface
  - Super type of `Generator.<T>`.
  - `proxy::has(v)`
  - `next():{done:Boolean, value:undefined|T}`
  - `toArray()`
  - Provides Array-like methods such as `map()` and `some()`.
- `INodeContainer.<T>`: interface for XML-like expressions such as `<C></C>`.
  - `INodeContainer_add(child:T):void`
- Final `DecoratorProperty`
  - `name:String`
  - `type:Class`
  - `writable:Boolean`
- `StringIndex`
  - Value class that represents a `String` index in different units: index in code points, `default`, and index in UTF-8 octets, `utf8`.
  - `source:String` is the string the `StringIndex` points to. This is neccessary to allow add and subtract operations.
  - `#default:Int`
  - `utf8:Int`
  - less than (`proxy::lt`)
  - greater than (`proxy::gt`)
  - less than or equals (`proxy::le`)
  - greater than or equals (`proxy::ge`)
  - `proxy::add(codePoints:Int):StringIndex` Adds `codePoints` to index based in the source string
  - `proxy::subtract(codePoints:Int):StringIndex` Subtracts `codePoints` to index based in the source string
- `GraphemeIndex`
 - Similiar to `StringIndex`, but also contains a `grapheme:Int` property.
- `String`
  - String is UTF-8.
  - `static fromCharCode()`
  - `'$a $$'.apply({ a: 10 })` (formatting function)
  - `'$1 $2'.apply(['one', 'two'])` (formatting function)
  - Index operator returns single-character `String` or empty `String` if out of bounds (accepts `Int|StringIndex|GraphemeIndex`)
  - `length` returns number of code points
  - `isEmpty`
  - `startIndex:StringIndex` (`{#default: 0, utf8: 0}`)
  - `endIndex:StringIndex`
  - `repeat()`
  - `replace()` similiar to EcmaScript
  - `match()` similiar to EcmaScript
  - `reverse()`
  - `split()` accepts string and `RegExp`
  - `indexOf()` returns `StringIndex?`
  - `lastIndexOf()` returns `StringIndex?`
  - `trim()`, `trimLeft()`, `trimRight()`
  - `startsWith()`, `endsWith()`
  - Read-only `firstChar:String` - returns first code point into string
  - Read-only `lastChar:String` - returns last code point into string (fast regardless of string length)
  - `proxy::iterateValues` yields code point `String`s
  - `chars` returns a `CharIterator`
  - `rightToLeftChars` returns a `RightToLeftCharIterator`
  - `charAt(index:Int|StringIndex)`
  - `charCodeAt(index:Int|StringIndex|GraphemeIndex)`
  - `slice(from:Int|StringIndex|GraphemeIndex, to:undefined|Int|StringIndex|GraphemeIndex = undefined)`
    - This method is always efficient regardless of string length if:
      - `from` is a `StringIndex` and `to` is `undefined`
      - `from` and `to` are `StringIndex`es.
  - `substr(index:Int|StringIndex|GraphemeIndex, length)`
    - `length` is in code points
  - `substring(from:Int|StringIndex|GraphemeIndex, to:undefined|Int|StringIndex|GraphemeIndex = undefined)`
    - This method is always efficient regardless of string length if:
      - `from` is a `StringIndex` and `to` is `undefined`
      - `from` and `to` are `StringIndex`es.
  - UTF-8 indexed operations
    - `lengthUTF8` number of octets
    - `octetAtUTF8(indexUTF8)`
    - `sizeAtUTF8(indexUTF8)`
    - `charAtUTF8(indexUTF8)`
    - `charCodeAtUTF8(indexUTF8)`
    - `sliceUTF8(fromUTF8Index, toUTF8Index = +Infinity)`
    - `substrUTF8(indexUTF8, length)`
      - `length` is in code points
    - `substringUTF8(fromUTF8Index, toUTF8Index = +Infinity)`
    - `indexToUTF8Index(index)`
    - `utf8IndexToIndex(index, skip:{initialIndexUTF8, initialIndex}? = null)`
      - The `skip` parameter can be specified for faster calculations given assumption that the previous indexes of the index to compute are known beforehand.
- `CharIterator`
  - Implements `Iterator.<Int>`
  - `index:StringIndex` writable
  - `hasRemaining`
  - Indexing (`s.chars[i]`) is equivalent to `peek(i)`
  - `peek(relativeIndex = 0)` relative index is given in code points; if negative, relative index is behind
  - `peekSequence(length:Int):String` length is in code points
  - `next()` yields `Int`
  - `skipSequence(length:Int)` length is in code points
  - `backward(length:Int = 1)`
  - `clone()`
- `RightToLeftCharIterator`
  - Implements `Iterator.<Int>`
  - `index:StringIndex` writable
  - Indexing (`s.rightToLeftChars[i]`) is equivalent to `peek(i)`
  - `peek(relativeIndex = 0)` relative index is given in code points; if negative, relative index is ahead
  - `peekSequence(length:Int):String` length is in code points, without inverting the string. For example, `'ecma'.rightToLeftChars.peekSequence(4)` equals `'ecma'`, not `'amce'`.
  - `next()` yields `Int`
  - `skipSequence(length:Int)` length is in code points
  - `forward(length:Int = 1)`
  - `clone()`
- `Function`
  - Extends `Class`
  - Basically used for untyped functions, but also a super type of typed functions.
- `Array.<T>`
  - `Array` does not implement `Iterator` because of the methods return type (return `Array` versus an abstract `Iterator`).
  - `first`
  - `last`
  - `reverse()` - mutates existing `Array`
  - `equals(anotherArray)`
  - `deepEquals(anotherArray)`
  - `insertAt(pos ,v):void`
  - `removeAt(pos):T|undefined`
  - Several other methods in EcmaScript
- `Stack.<T>`
  - `peek():undefined|T`
  - `push()`
  - `pop()`
- `Queue.<T>`
  - `peek():undefined|T`
  - `enqueue(v:T)` adds value to the end of the queue
  - `dequeue():undefined|T` removes and returns the value at the beginning of the queue, or returns `undefined` if empty
- `Map.<K, V>`
  - `length`
  - Items ordered by insertion.
  - Clone constructor (`new Map(anotherMap)`)
- `WeakMap.<K, V>`
  - `length`
  - Items ordered by insertion.
  - Clone constructor (`new WeakMap(anotherMap)`)
- `Set.<T>`
  - `length`
  - Items ordered by insertion.
  - Clone constructor (`new Set(anotherSet)`)
- `WeakSet.<T>`
  - `length`
  - Items ordered by insertion.
  - Clone constructor (`new WeakSet(anotherSet)`)
- `Promise.<T>`
- `Generator.<T>`
  - Subtype of `Iterator.<T>`
- `undefined`
- `Infinity`
- `NaN`
- `Class` (not final)
- `ByteArray`
- `Intl` namespace
- `Math` namespace
- `Reflect` namespace
  - `construct(o:*, arguments:[*]):*`
  - `describeFunction(f:Function):violetscript.meta.Function`
  - `describeType(type:Class):violetscript.meta.Type`
  - `getConstructorOf(o:*):Class?`
  - `get(o:*, k:String):*`
  - `set(o:*, k:String, v:*):Boolean`
- `violetscript.meta.Binding`
  - `name:String`
  - `type:Class`
- `violetscript.meta.VariableProperty`
- `violetscript.meta.VirtualProperty`
- `violetscript.meta.Function`
  - `requiredParams:[violetscript.meta.Binding]?`
  - `optParams:[violetscript.meta.Binding]?`
  - `restParam:violetscript.meta.Binding?`
  - `returnType:Class`
- `violetscript.meta.Type`
  - `violetscript.meta.AnyType`
  - `violetscript.meta.UndefinedType`
  - `violetscript.meta.NullType`
  - `violetscript.meta.ClassType`
  - `violetscript.meta.EnumType`
  - `violetscript.meta.InterfaceType`
  - `violetscript.meta.InstantiationType`
  - `violetscript.meta.UnionType`
  - `violetscript.meta.TupleType`
  - `violetscript.meta.RecordType`
  - `violetscript.meta.FunctionType`
  - `violetscript.meta.TypeParameter`
- `Temporal` namespace
  - Based on https://tc39.es/proposal-temporal/docs
- `JSON`
- `Boolean`
- `Number`
  - static `range(start, end, step?):Iterator.<Number>`
- `Decimal`
  - static `range(start, end, step?):Iterator.<Decimal>`
- `Byte`
  - static `range(start, end, step?):Iterator.<Byte>`
- `Short`
  - static `range(start, end, step?):Iterator.<Short>`
- `Int`
  - static `range(start, end, step?):Iterator.<Int>`
- `Long`
  - static `range(start, end, step?):Iterator.<Long>`
- `BigInt`
  - static `range(start, end, step?):Iterator.<BigInt>`
- `Object`
- `RegExp`
  - Supports the flag `x` for ignoring whitespace and line breaks
  - Supports `\p{...}` and `\u{...}`.
  - Matched capture groups get a `StringIndex` record.
- `Boxed.<T>`
  - Serves as a reference-type wrapper for value types, generally useful for wrapping records and tuples.
  - `Boxed(v)`
  - `valueOf():T`
- `IDisposable` interface
  - `dispose():void`
- `trace()`
- `parseInt()`
- `parseFloat()`
- `encodeURI()`
- `decodeURI()`
- `encodeURIComponent()`
- `decodeURIComponent()`
- `isNaN()`
- `isFinite()`

For desambiguation purpose:

- `global` (refers to the top-level package)
  - This can be used to refer to a package or top-level definition that starts with a scope conflicting name. For example:
```
var com = 10;
global.com.qux.f();
// another example
const Infinity = 10;
var x = Infinity;
var y = global.Infinity;
```

Error:

- `Error`
- `ArgumentError`
- `AssertionError`
- `RangeError`
- `ReferenceError`

Assertion:

- `assert()`
- `assertEquals()`
- `assertNotEquals()`
- `assertThrows()`
- `assertDoesntThrow()`

## Future built-ins

- `String`
  - `graphemes`
  - `rightToLeftGraphemes`
- `GraphemeIterator`
- `RightToLeftGraphemeIterator`