# Statements

## Declarations

Decorators:

- `[Blah] var x = 10;`
- Decorators are indentation-based, thus the following code automatically inserts semicolon properly:

```
// o[10]
o
    [10]

// f()
f()
[Value]
class C {
}
```

Packages: (top-level-only; packages are not annotatable definitions)

```
package bar.qux {
    public var x = 0;
}
package {
    // top-level
}
{
    // qux is undefined
    import bar.*;
    // qux is still undefined
}
```

Namespaces:

```
namespace Tp = Temporal;
// package alias
namespace Bq = bar.qux;

namespace Q {
    var x = 0;
}
```

Variables:

```
var x = 0;
const x = 0; // shadows previous 'x'

{
    var y = 0;
}
// y is undefined out of this block, since variables are block-scoped
```

Functions:

```
function f():void {
}
```

Classes:

```
class C {
}
```

Interfaces:

```
interface I {
}
```

Enumerations:

```
enum E {
}
```

Types:

```
type T = ToBeAliased;
```

## Uncategorized

- `expression;`
- `;` (empty statement)
- `{}` (block)
- `super(...)`
- `import`
  - `import q.**;` (recursive: imports `q` and subpackages)
  - `import q.u.B;`
  - `import q.u.*;`
  - `import A = q.u.B;`
  - `import Qu = q.u.*;`
- `if (c) ...;`
  - Accepts simple variable declaration:
```
if (var o = o as C) {
    // procedure
}
```
- `do ...; while (c);`
- `while (c) ...;`
  - Accepts simple variable declaration:
```
while (var o:C? = o as C) {
    // procedure
}
```
- `break ...;`
- `continue ...;`
- `return ...;`
- `throw error;`
- `try`
- `label: ...` (labeled statement)
- `for (i; c; u) ...;`
- `for (i in o) ...;`
  - Works with object with `iterateKeys()` proxy.
- `for each (v in o) ...;`
  - Works with object with `iterateValues()` proxy.
  - Works with Generator object.
  - Works with Iterator object.
- `switch`
  - Unlike ECMAScript, `case`s do not fallback, so there is no need for explicit `break` statements
- `switch type (v) { case (n:Number) {} }`
  - Supports default case `switch type (v) { default() {} }`
  - When applied to an algebraic data class, must cover all subtypes if no `default` case is supplied.
- `include './src.es';`
  - Causes statement sequence from a given source to be part of the current statement sequence. This statement does not concatenate source to source, diverging from ActionScript.
- `use namespace someNS;`
- `use resource (...) {}` (uses the `IDisposable` interface)
- `with (o) ...;`