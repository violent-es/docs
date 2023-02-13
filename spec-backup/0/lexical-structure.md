# Lexical structure

Comments:

- `// single line`
- `/* multi-line /* nested */ */`
- `<!-- XML-like comment -->`

Literal:

- Triple-quote string: `'''-'''`, indent-aware based on last `'''` and consumes first and last line break.
- Regular expression `/b/f`
- Null: `null`
- Boolean: `false, true`
- Numeric: `0`, `0x...`, `0b...`
  - Allow underscore separator: `_`

Identifier:

- `nonReservedWordId`
- `#possiblyReservedWordId`
  - First character can be any `IdentifierPart`, like `#3D_WORLD`.
- May contain `\x{...}` and `\u{...}`
- After dot and `?.`, for member operator, is allowed a `reservedWordId`.

Punctuators:

- `{`
- `}`
- `[`
- `]`
- `(`
- `)`
- `.`
- `?.`
- `...`
- `;`
- `,`
- `<`
- `>`
- `</` (for node initializer)
- `<=`
- `>=`
- `==`
- `!=`
- `===`
- `!==`
- `+`
- `-`
- `*`
- `/`
- `%`
- `**`
- `++`
- `--`
- `<<`
- `>>`
- `>>>`
- `&`
- `|`
- `^`
- `!`
- `~`
- `&&`
- `^^`
- `||`
- `??`
- `?`
- `:`
- `->`
- `=`
- `+=`
- `-=`
- `*=`
- `/=`
- `%=`
- `**=`
- `<<=`
- `>>=`
- `>>>=`
- `&=`
- `^=`
- `|=`
- `&&=`
- `^^=`
- `||=`
- `??=`

Reserved words:

- `as`
- `await`
- `break`
- `case`
- `catch`
- `class`
- `const`
- `continue`
- `default`
- `delete`
- `do`
- `else`
- `extends`
- `finally`
- `for`
- `function`
- `if`
- `implements` 
- `import`
- `in`
- `interface`
- `internal`
- `is`
- `new`
- `package`
- `private`
- `protected`
- `public`
- `return`
- `super`
- `switch`
- `this`
- `throw`
- `throws`
- `try`
- `typeof`
- `use`
- `var`
- `void`
- `where`
- `while`
- `with`
- `yield`

Context keywords:

- `each`
  - Used for for..in that iterates values
- `embed`
  - Used for embed expression
- `enum`
  - Used for enum declarations
- `final`
  - Annotatable definition modifier
- `get`
  - Used for getter declarations
- `include`
  - Used for include directive
- `meta`
  - Used for `import.meta`
- `namespace`
  - Used for namespace definitions
- `native`
  - Annotatable definition modifier
- `override`
  - Annotatable definition modifier
- `proxy`
  - Used for proxy declarations
- `resource`
  - Used by `use resource` statement
- `set`
  - Used for setter declarations
- `static`
  - Annotatable definition modifier
- `type`
  - Used for type declarations
- `undefined`
  - Used for undefined type expression
- `wraps`
  - Used for enumeration definitions.