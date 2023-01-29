# Built-in Objects

## global

This is a property that refers to the global package.

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