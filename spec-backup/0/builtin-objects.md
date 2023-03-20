# Built-in Objects

## global

This is a property that refers to the global package.

This can be used to refer to a package or top-level definition that starts with a lexically conflicting name. For example:

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

## IMarkupContainer.\<T>

Interface for markup expressions such as `<C></C>`.

**Methods:**

- `IMarkupContainer_add(child:T):void`

## StringIndex

Value class that represents a `String` index in different units: index in code points, `default`, and index in UTF-8 octets, `utf8`.

**Properties:**

- `source:String`: The string the index was extracted from.
- `default:Int`
- `utf8:Int`

**Proxies:**

- less than (`proxy::lt`)
- greater than (`proxy::gt`)
- less than or equals (`proxy::le`)
- greater than or equals (`proxy::ge`)
- `proxy::add(codePoints:Int):StringIndex`: Adds `codePoints` to index based in the source string
- `proxy::subtract(codePoints:Int):StringIndex`: Subtracts `codePoints` to index based in the source string

## GraphemeIndex

Similiar to StringIndex, but with a `graphemes` property. Operations such as addition and subtraction are in graphemes.

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
- `apply(arguments:Map.<String, *>|[*]):String`: Formats arguments.
  - `'$a $$'.apply({ a: 10 })`
  - `'$1 $2'.apply(['one', 'two'])`
  - `'$<IE_bar>'.apply(...)` allows name with hyphen and underscore
  - Internally used regular expression: `/\$([a-z0-9]+|<[a-z_\-0-9]+>|\$)/gi`
  - Futurely we can support advanced parameters with formatting options, such as:
    - `${name=qux,x=y,z=w}`
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

(Final.)

`Array` does not implement `Iterator` because of the methods return type (return `Array` versus an abstract `Iterator`).

**Properties:**

- `first:undefined|T`
- `last:undefined|T`
- `length:Int`

**Proxies:**

- Indexing (including `delete`)
- `in` operator (determines if the `Array` includes a value)
- `for each`

**Methods:**

- `reverse()` - mutates existing `Array`
- `equals(anotherArray)`
- `deepEquals(anotherArray)`
- `insertAt(pos ,v):void`
- `removeAt(pos):undefined|T`
- Several other methods in EcmaScript

## Stack.\<T>

(Final.)

**Properties:**

- `length`

**Methods:**

- `peek():undefined|T`
- `push()`
- `pop()`
- `values():Iterator.<T>`

## Queue.\<T>

(Final.)

**Properties:**

- `length`
- `values():Iterator.<T>`

**Methods:**

- `peek():undefined|T`
- `enqueue(v:T)`: Adds value to the end of the queue
- `dequeue():undefined|T`: Removes and returns the value at the beginning of the queue, or returns `undefined` if empty

## Map.\<K, V>

(Final.)

Items are ordered by insertion.

**Constructor:**

- `new Map`
- `new Map(entries:[K, V])`
- `new Map(anotherMap)`: Clones another Map object.

**Properties:**

- `length`
- `entries():Iterator.<[K,V]>`
- `keys():Iterator.<K>`
- `values():Iterator.<V>`

## WeakMap.\<K, V>

(Final.)

Similiar to Map, but with weak key references.

## Set.\<T>

(Final.)

Items are ordered by insertion.

**Proxies:**

- `for each`
- `in`

**Properties:**

- `length`

**Methods:**

- `add(v:T):void`
- `delete(v:T):Boolean`
- `values():Iterator.<T>`

## WeakSet.\<T>

(Final.)

Similiar to Set.

## Promise.\<T>

(Final.)

## Generator.\<T>

(Final.)

**Implements:** Iterator.\<T>

## undefined

## NaN

## Infinity

## Class

(Non-final.)

Represents any type.

## ByteArray

(Final.)

## Intl (namespace)

## Math (namespace)

## Reflect (namespace)

**Methods:**

- `construct(o:*, arguments:[*]):*`
- `typeOf(type:Class):Object`
  - Returns a type meta-object describing the given type.
- `get(o:*, k:String):*`
- `set(o:*, k:String, v:*):Boolean`

## "Type meta-objects"

Type meta-objects describe types at runtime.

- Binding
  - Represents general name bindings, including variable and virtual properties and methods. Also used for decorated properties.
  - `name:String`
  - `type:Class`
  - `readOnly:Boolean`
  - `writable:Boolean`
- AnyType
- UndefinedType
- NullType
- ArrayType
  - Represents an instantiation of the Array class.
- ClassType
- EnumType
- InterfaceType
- InstantiationType
- UnionType
- TupleType
- RecordType
- FunctionType
  - `requiredParams:[Binding]?`
  - `optParams:[Binding]?`
  - `restParam:Binding?`
  - `returnType:Class`
- TypeParameter

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

**Properties:**

- `constructor:Class`: read-only reference to the constructor type of an object.

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
- `TypeError`

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