# Built-in Objects

## global

This is a property that refers to the global package.

This can be used to refer to a package or top-level definition that starts with a scope conflicting name. For example:

```
var com = 10;
global.com.qux.f();
// another example
const Infinity = 10;
var x = Infinity;
var y = global.Infinity;
```

## Iterator.\<T>

**Extends:** Generator.\<T>

**Proxies:**

- `proxy::has`: tests if value is contained in a collection

**Methods:**

- `next():{done:Boolean, value:undefined|T}`
- `toArray():[T]`
- Array-like functional methods such as `map()` and `some()`

## INodeContainer.\<T>

Interface for markup expressions such as `<C></C>`.

**Methods:**

- `INodeContainer_add(child:T):void`

## DecoratorProperty

**Properties:**

- `name:String`
- `type:Class`
- `writable:Boolean`

## StringIndex

**Properties:**

- `source:String`: The string the index was extracted from.
- `#default:Int`
- `utf8:Int`

**Proxies:**

- less than (`proxy::lt`)
- greater than (`proxy::gt`)
- less than or equals (`proxy::le`)
- greater than or equals (`proxy::ge`)
- `proxy::add(codePoints:Int):StringIndex`: Adds `codePoints` to index based in the source string
- `proxy::subtract(codePoints:Int):StringIndex`: Subtracts `codePoints` to index based in the source string

## GraphemeIndex

Similiar to StringIndex, but `#default` is in graphemes and provides a `codePoints` index. Operations such as addition and subtraction are in graphemes.

## String

The String data type is UTF-8 encoded, but it is manipuled by code points.

**Properties:**

- `length:Int`: Returns number of code points.
- `isEmpty:Boolean`: Determines if the String has no octets.
- `startIndex:StringIndex`
- `endIndex:StringIndex`
- `firstChar:String`
- `lastChar:String`: Returns last code point String. The implementation should skip directly to last character.

**Proxies:**

- Index operator: Yields single-character String or empty string if out of bounds. Accepts `Int|StringIndex|GraphemeIndex`.
- Addition (`proxy::add(other:*):String`)
- `for each`: Yields code point Strings.

**Methods:**

- `static fromCharCode(...):String`
- `apply(arguments:Map.<String, String>|[String]):String`: Formats arguments.
  - `'$a $$'.apply({ a: 10 })`
  - `'$1 $2'.apply(['one', 'two'])`
  - Parameter `RegExp`: `/\$([a-z0-9]+|\$)/gi`
- `repeat()`
- `replace()`: Similiar to EcmaScript
- `match()`: Similiar to EcmaScript
- `reverse()`
- `split()`: Accepts String and RegExp
- `indexOf():StringIndex?`
- `lastIndexOf():StringIndex?`
- `trim()`
- `trimLeft()`
- `trimRight()`
- `startsWith()`
- `endsWith()`
- `chars:CharIterator`
- `rightToLeftChars:RightToLeftCharIterator`
- `charAt(index:Int|StringIndex):String`
- `charCodeAt(index:Int|StringIndex|GraphemeIndex):Int`
- `slice(from:Int|StringIndex|GraphemeIndex, to:undefined|Int|StringIndex|GraphemeIndex = undefined):String`
  - This method is always efficient regardless of string length if:
    - `from` is a `StringIndex` and `to` is `undefined`
    - `from` and `to` are `StringIndex`es.
- `substr(index:Int|StringIndex|GraphemeIndex, length:Int):String`
  - `length` is in code points
- `substring(from:Int|StringIndex|GraphemeIndex, to:undefined|Int|StringIndex|GraphemeIndex = undefined):String`
  - This method is always efficient regardless of string length if:
    - `from` is a `StringIndex` and `to` is `undefined`
    - `from` and `to` are `StringIndex`es.

## UTF8 (namespace)

**Methods:**

- `static length(str)` = number of octets
- `static octetAt(str, indexUTF8)`
- `static sizeAt(str, indexUTF8)`
- `static charAt(str, indexUTF8)`
- `static charCodeAt(str, indexUTF8)`
- `static slice(str, fromUTF8Index, toUTF8Index = +Infinity)`
- `static substr(str, indexUTF8, length)`
  - `length` is in code points
- `static substring(str, fromUTF8Index, toUTF8Index = +Infinity)`
- `static indexToUTF8Index(str, index)`
- `static utf8IndexToIndex(str, index, skip:{initialIndexUTF8, initialIndex}? = null)`
  - The `skip` parameter can be specified for faster calculations given assumption that the previous indexes of the index to compute are known beforehand.

## CharIterator

**Implements:** Iterator.\<Int>

**Properties:**

- `index:StringIndex`: Writable
- `hasRemaining:Boolean`

**Proxies:**

- Indexing (`s.chars[i]`): Equivalent to `s.peek(i)`

**Methods:**

- `peek(relativeIndex = 0)`: Relative index is given in code points; if negative, relative index is behind
- `peekSequence(length:Int):String`: Length is in code points
- `next()`: Yields `Int`
- `skipSequence(length:Int)`: Length is in code points
- `backward(length:Int = 1)`
- `clone()`

## RightToLeftCharIterator

- `index:StringIndex`: Writable
- `hasRemaining:Boolean`

**Proxies:**

- Indexing (`s.rightToLeftChars[i]`): Equivalent to `s.peek(i)`

**Methods:**

- `peek(relativeIndex = 0)`: Relative index is given in code points; if negative, relative index is ahead
- `peekSequence(length:Int):String`: Length is in code points, without inverting the String. For example, `'ecma'.rightToLeftChars.peekSequence(4)` equals `'ecma'`, not `'amce'`.
- `next()`: Yields `Int`
- `skipSequence(length:Int)`: Length is in code points
- `forward(length:Int = 1)`
- `clone()`

## Function

Basically used for untyped functions, but also a super type of structural function types.

**Extends:** Class

## Array.\<T>

`Array` does not implement `Iterator` because of the methods return type (return `Array` versus an abstract `Iterator`).

**Properties:**

- `first`
- `last`
- `length`

**Proxies:**

- Indexing (including `delete`)
- `for each`

**Methods:**

- `reverse()` - mutates existing `Array`
- `equals(anotherArray)`
- `deepEquals(anotherArray)`
- `insertAt(pos ,v):void`
- `removeAt(pos):undefined|T`
- Several other methods in EcmaScript

## Stack.\<T>

**Properties:**

- `length`

**Methods:**

- `peek():undefined|T`
- `push()`
- `pop()`

## Queue.\<T>

**Properties:**

- `length`

**Methods:**

- `peek():undefined|T`
- `enqueue(v:T)`: Adds value to the end of the queue
- `dequeue():undefined|T`: Removes and returns the value at the beginning of the queue, or returns `undefined` if empty

## Map.\<K, V>

Items are ordered by insertion.

**Constructor:**

- `new Map`
- `new Map(entries:[K, V])`
- `new Map(anotherMap)`: Clones another Map object.

**Properties:**

- `length`

## WeakMap.\<K, V>

Similiar to Map, but with weak key references.

## Set.\<T>

Items are ordered by insertion.

**Proxies:**

- `for each`
- `in`

**Properties:**

- `length`

**Methods:**

- `add(v:T):void`
- `#delete(v:T):Boolean`

## WeakSet.\<T>

Similiar to Set.

## Promise.\<T>

## Generator.\<T>

**Implements:** Iterator.\<T>

## undefined

## NaN

## Infinity

## Class

Not final.

## ByteArray

## Intl (namespace)

## Math (namespace)

## Reflect (namespace)

**Methods:**

- `construct(o:*, arguments:[*]):*`
- `describeFunction(f:Function):violetscript.meta.Function`
- `describeType(type:Class):violetscript.meta.Type`
- `constructorOf(o:*):Class?`
- `get(o:*, k:String):*`
- `set(o:*, k:String, v:*):Boolean`

## violetscript.meta.Binding

**Properties:**

- `name:String`
- `type:Class`

## violetscript.meta.VariableProperty

## violetscript.meta.VirtualProperty

## violetscript.meta.Function

**Properties:**

- `requiredParams:[violetscript.meta.Binding]?`
- `optParams:[violetscript.meta.Binding]?`
- `restParam:violetscript.meta.Binding?`
- `returnType:Class`

## violetscript.meta.Type

**Subtypes:**

- violetscript.meta.AnyType
- violetscript.meta.UndefinedType
- violetscript.meta.NullType
- violetscript.meta.ClassType
- violetscript.meta.EnumType
- violetscript.meta.InterfaceType
- violetscript.meta.InstantiationType
- violetscript.meta.UnionType
- violetscript.meta.TupleType
- violetscript.meta.RecordType
- violetscript.meta.FunctionType
- violetscript.meta.TypeParameter

## Temporal (namespace)

Based on https://tc39.es/proposal-temporal/docs.

## JSON (namespace)

## Boolean

## Number

**Methods:**

- `static range(start, end, step?):Iterator.<Number>`

## Decimal

**Methods:**

- `static range(start, end, step?):Iterator.<Decimal>`

## Byte

**Methods:**

- `static range(start, end, step?):Iterator.<Byte>`

## Short

**Methods:**

- `static range(start, end, step?):Iterator.<Short>`

## Int

**Methods:**

- `static range(start, end, step?):Iterator.<Int>`

## Long

**Methods:**

- `static range(start, end, step?):Iterator.<Long>`

## BigInt

**Methods:**

- `static range(start, end, step?):Iterator.<BigInt>`

## Object

## RegExp

**Features:**

- Supports the flag `x` for ignoring whitespace and line breaks
- Supports `\p{...}` and `\u{...}`.
- Matched capture groups get a `StringIndex` record.

## Boxed.\<T>

Boxed is currently undefined. In the future it may be used to indicate that a structural record or tuple is a mutable object reference.

## IDisposable.\<T>

Used by the `use resource` statement.

**Methods:**

- `dispose():void`

## trace()

## parseInt()

## parseFloat()

## encodeURI()

## decodeURI()

## encodeURIComponent()

## decodeURIComponent()

## isNaN()

## isFinite()

## Error

**Subtypes:**

- `ArgumentError`
- `AssertionError`
- `RangeError`
- `ReferenceError`

## Assertion Functions

Assertion functions:

- `assert()`
- `assertEquals()`
- `assertNotEquals()`
- `assertThrows()`
- `assertDoesntThrow()`

## Future Built-ins

- `String`
  - `graphemes`
  - `rightToLeftGraphemes`
- `GraphemeIterator`
- `RightToLeftGraphemeIterator`