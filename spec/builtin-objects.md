# Built-in Objects

This list of built-ins is incomplete. It doesn't document many of the JavaScript standard built-ins, but the language will implement most of them.

## global

This is a property that refers to the global package.

This can be used to refer to a package or top-level definition that starts with a lexically conflicting name. For example:

```
const com = 10;
global.com.qux.f();

// another example
const Infinity = 10;
const x = Infinity;
const y = global.Infinity;
```

## Iterator.\<T>

**Methods:**

- `next(): {done: Boolean, value: undefined | T}`
- Array-like functional methods such as `map()` and `some()`

## IMarkupContainer.\<T>

Interface for markup expressions such as `<C></C>`.

**Methods:**

- `IMarkupContainer_add(child: T): void`

## String

The String data type is UTF-16 encoded for compatibility with the ECMA-262 String type.

**Properties:**

- `length: Int`: Returns number of code points.
- `isEmpty: Boolean`

**Proxies:**

- Index operator: Yields single Code Point character string or empty string if out of bounds.
- Addition (`proxy::add(other: *): String`)
- Iterator: Yields code point Strings.

**Methods:**

- `static fromCharCode(...): String`
- `static fromCodePoint(...): String`
- `apply(arguments: Map.<String, *> | [*]): String`: Formats arguments.
  - `'$a $$'.apply({ a: 10 })`
  - `'$1 $2'.apply(['one', 'two'])`
  - `'$<hyphens-n_Underscores>'.apply(...)`
  - Internally used regular expression: `/\$([a-z0-9]+|<[a-z_\-0-9]+>|\$)/gi`
  - Futurely we can support advanced parameters with formatting options, such as:
    - `${param=paramName,x=y,z=w}`
- `repeat()`
- `replace()`: Similiar to EcmaScript
- `match()`: Similiar to EcmaScript
- `reverse()`
- `split()`: Accepts String and RegExp
- `indexOf(): Int`
- `lastIndexOf(): Int`
- `trim()`
- `trimLeft()`
- `trimRight()`
- `startsWith()`
- `endsWith()`
- `codePoints(): CodePointIterator`
- `rightCodePoints(): RightCodePointIterator`
- `charAt(index: Int): String`
- `charCodeAt(index: Int): Int`
- `codePointAt(index: Int): Int`
- `slice(from: Int, to?: Int?): String`
- `substr(index: Int, length?: Int?): String`
- `substring(from: Int, to?: Int?): String`

## CodePointIterator

**Implements:** Iterator.\<Int>

**Properties:**

- `index: Int`: Writable
- `hasRemaining: Boolean`

**Proxies:**

- Indexing (`s.chars[i]`): Equivalent to `s.peek(i)`

**Methods:**

- `peek(relativeIndex = 0)`: Relative index is given in code points; if negative, relative index is behind
- `peekSeq(length: Int):String`: Length is in code points
- `nextCodePoint(): Int`: If end reached, returns zero.
- `skip(length: Int)`: Length is in code points
- `backward(length: Int = 1)`
- `clone()`

## RightCodePointIterator

**Implements:** Iterator.\<Int>

**Properties:**

- `index: Int`: Writable
- `hasRemaining: Boolean`

**Proxies:**

- Indexing (`s.RightChars[i]`): Equivalent to `s.peek(i)`

**Methods:**

- `peek(relativeIndex = 0)`: Relative index is given in code points; if negative, relative index is ahead
- `peekSeq(length: Int): String`: Length is in code points, without inverting the String. For example, `'ecma'.rightCodePoints().peekSequence(4)` equals `'ecma'`, not `'amce'`.
- `nextCodePoint(): Int`: If end reached, returns zero.
- `skip(length: Int)`: Length is in code points
- `clone()`

## Function

Basically used for untyped functions, but also a super type of structural function types.

**Extends:** Class

## Array.\<T>

(Final.)

`Array` does not implement `Iterator` because of the methods return type (return `Array` versus an abstract `Iterator`).

**Properties:**

- `first: undefined | T`
- `last: undefined | T`
- `length: Int`

**Proxies:**

- Indexing (including `delete`)
- `in` operator (determines if the `Array` includes a value)
- Iterator

**Methods:**

- Static `from(iterator)`
- `reverse()` - mutates existing `Array`
- `forEach(fn)`
- `equals(anotherArray)`
- `deepEquals(anotherArray)`
- `insertAt(pos, v): void`
- `removeAt(pos): undefined | T`
- Several other methods in EcmaScript

## Stack.\<T>

(Final.)

**Proxies:**

- Iterator
- `in`

**Properties:**

- `length`

**Methods:**

- `peek(): undefined | T`
- `push()`
- `pop()`

## Queue.\<T>

(Final.)

**Proxies:**

- Iterator
- `in`

**Properties:**

- `length`

**Methods:**

- `peek(): undefined | T`
- `enqueue(v: T)`: Adds value to the end of the queue
- `dequeue(): undefined | T`: Removes and returns the value at the beginning of the queue, or returns `undefined` if empty

## Map.\<K, V>

(Final.)

Items are ordered by insertion.

**Constructor:**

- `new Map`
- `new Map(entries: [K, V])`
- `new Map(anotherMap)`: Clones another Map object.
- `new Map(anotherWeakMap)`

**Proxies:**

- Iterator (yields `[K, V]`)
- `in`
- Get index
- Set index
- Delete index

**Properties:**

- `length`

**Methods:**

- `entries(): Iterator.<[K, V]>`
- `keys(): Iterator.<K>`
- `values(): Iterator.<V>`
- `forEach(fn)`

## WeakMap.\<K, V>

(Final.)

Similiar to Map, but with weak key references.  Constructor too.

## Set.\<T>

(Final.)

Items are ordered by insertion.

**Constructor:**

- `new Set`
- `new Set(values: [V])`
- `new Set(anotherSet)`: Clones another Set object.
- `new Set(anotherWeakSet)`

**Proxies:**

- Iterator
- `in`

**Properties:**

- `length`

**Methods:**

- `add(v: T): void`
- `delete(v: T): Boolean`
- `values(): Iterator.<T>`

## WeakSet.\<T>

(Final.)

Similiar to Set. Constructor too.

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

**Methods:**

- [ ] `clamp(value:*, min:*, max:*):*`

## Reflect (namespace)

**Methods:**

- `construct(o : *, arguments : [*]) : *`
- `typeOf(type : Class) : Object`
  - Returns a type meta-object describing the given type.
- `get(o : *, k : String) : *`
- `set(o : *, k : String, v : *) : Boolean`

## "Type meta-objects"

Type meta-objects describe types at runtime.

- Binding
  - Represents general name bindings, including variable and virtual properties and methods. Also used for decorated properties.
  - `name : String`
  - `type : Class`
  - `readOnly : Boolean`
  - `writable : Boolean`
- AnyType
- UndefinedType
- NullType
- ArrayType
  - Represents an instantiation of the Array class.
- ClassType
- EnumType
- InterfaceType
- TypeWithArguments
- UnionType
- TupleType
- RecordType
- FunctionType
  - `requiredParams : [Binding]?`
  - `optParams : [Binding]?`
  - `restParam : Binding?`
  - `returnType : Class`
- TypeParameter

## Temporal (namespace)

Based on https://tc39.es/proposal-temporal/docs.

## JSON (namespace)

## Boolean

## Number

**Methods:**

- `static range(start, end, step?): Generator.<Number>`

## Decimal

**Methods:**

- `static range(start, end, step?): Generator.<Decimal>`

## Byte

**Methods:**

- `static range(start, end, step?): Generator.<Byte>`

## Short

**Methods:**

- `static range(start, end, step?): Generator.<Short>`

## Int

**Methods:**

- `static range(start, end, step?): Generator.<Int>`

## Long

**Methods:**

- `static range(start, end, step?): Generator.<Long>`

## BigInt

**Methods:**

- `static range(start, end, step?): Generator.<BigInt>`

## Object

**Properties:**

- `constructor: Class`: read-only reference to the constructor type of an object.

## RegExp

**Features:**

- Supports the flag `x` for ignoring whitespace and line breaks
- Supports `\p{...}` and `\u{...}`.

## Boxed.\<T>

Boxed is currently undefined. In the future it may be used to indicate that a structural record or tuple is a mutable object reference.

## IDisposable.\<T>

Used by the `use resource` statement.

**Methods:**

- `dispose(): void`

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
- `IOError`

## Assertion Functions

Assertion functions:

- `assert()`
- `assertEqual()`
- `assertNotEqual()`
- `assertThrows()`