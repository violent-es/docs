# Types

## Enum

Enum constants consist of a String and a number (of type `Int` by default).

Default enums:

```
enum Product {
    // ['smartphone', 0]
    const SMARTPHONE;

    // ['aUtOmObIlE', 1]
    const AUTOMOBILE = 'aUtOmObIlE';

    // ['kxxx', 65]
    const KEYBOARD = [65, 'kxxx'];

    function customMethod():void {
    }
}

var p:Product = 'kxxx';
var p:Product = Product.KEYBOARD;
p.valueOf(); // 65
p.toString(); // 'kxxx'
p = Product(65);
p = Product('kxxx');

var t:Product? = 65 as? Product;
```

Flags enums:

```
[Flags]
enum Permissions {
    // ['fooBlah', 1]
    const FOO_BLAH;

    // ['qux', 2]
    const QUX;

    // ['baz', 4]
    const BAZ;
}

var p:Permissions = ['fooBlah', 'qux'];
p = {fooBlah: true, baz: false};
p = p.toggle('fooBlah');
p = p.filter('qux');
p += 'qux';
p -= 'qux';
'qux' in p;

// empty
p = undefined;
p = {};
p = [];

// include all flags
p = Permissions.all;
```

Custom numeric type:

```
enum E wraps BigInt {
}
```

### Flag exclusion

The expression `flag1 - flag2` is equivalent to `F(flag1.valueOf() & ~flag2.valueOf())`.

## Classes

Value classes are final and mustn't extend or implement types.

```
package foo.bar {
    [Value]
    public class Vector2D {
        // members are always read-only
        public const x:Number;
        public const y:Number;
        public function Vector2D(x:Number, y:Number) {
            // initialize members at constructor
            this.x = x;
            this.y = y;
        }
    }
}
```

## Interfaces

```
interface A {
}
```

Interfaces support both required and optional methods.

## Inheritance

Definitions marked `static` will be inherited across subclasses.

## Primitive

- `Boolean`
- `String`
  - Differently from EcmaScript, strings are UTF-8 encoded
- `Number`
- `Decimal`
- `Byte`
  - Unsigned 8-bit integer
- `Short`
  - Signed
- `Int`
  - Signed
- `Long`
  - Signed
- `BigInt`
  - Signed

## Any

```
type Any = *;
var o:*;
o.x = 10; // dynamic: x is resolved at runtime
```

## Void or undefined

```
function f():void {}

// record with optional option defaulting to undefined.
// undefined is a context keyword for type expressions.
type Options = {
    optionalOption:undefined|String,
};

var options:Options = {};
options.optionalOption; // undefined
```

## Null

```
var nullVar:* = null;

// both are equivalent
var s:null|String;
var s:String?;
```

## Function

```
type F = function(a:Number):void;
```

Arrow functions are equivalent to conventional functions, but shorter:

```
type F = (a:Number)=>void;
```

## Tuple

Tuples are passed and compared by value.

```
type TupleA = [Boolean, Number];
```

## Record

Records are passed and compared by value.

```
type RecordA = {x:Number, y:Number};
```

If field type contains `undefined` or `null`, the field is optional and may be omitted in an object initializer. If field type contains both `undefined` and `null`, `undefined` is used as default value.

### Record type field ordering

Record types whose fields intersect each other are different depending on the order of each field. For example, in the following program, `X` and `Y` are different types, due to the order in which each field appears:

```
type X = {x:Number, y:Number};
type Y = {y:Number, x:Number};
```

The order of the fields in an object initializer does not matter:

```
var o:X = {y: 0, x: 0};
var o:Y = {x: 0, y: 0};
```

## Union

```
// vertical line
type DToN =
    | Temporal.ZonedDateTime
    | Number
    ;
```

Special cases:

- If union expression contains the type `*`, it returns `*`.
- If union expression contains another union, they are combined.

### Union type's member ordering

Unions with same set of members can be different depending on the order of members. In the following program, `U1` and `U2` are different types:

```
type U1 = undefined|String;
type U2 = String|undefined;
```

## Array

```
// following type expressions are equivalent
type ArrayOfInt = [Int];
type ArrayOfInt2 = Array.<Int>;
```

## Instantiated type

```
type SomeInstantiation = C.<Number>;
```

## Type parameter

```
class C.<T> {
    var v:T; // T is a type parameter
}
```

## Nullable

```
type N = Int?; // returns a null|Int union
```

## Non-nullable

```
type Nn = Object!;
```

If the operand type is `*` or `null`, the type remains the same.

## Nullability

The types `*` and `null|...` contain `null`. All other types are non-nullable.

## Truthy value

`undefined`, `null`, `false`, `0`, `NaN`, `''` and empty flags are falsy values. All other values are truthy.