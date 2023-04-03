# Optimizations

- `array.push(v);`: takes only one argument, so do not create an `Array` for rest arguments.
- `for each (var i in Number.range(0, 10) ...;`: optimize loop by skipping `Generator` instance and skipping step parameter.
- `Boxed` dereferencing property access and method call. For example, `o.valueOf().x` should access `x` without reallocating the value in the stack.
- `String` is internally either original or a slice of another one.
- `str.length == 0`: uses `isEmpty`
- `str.length != 0`: uses `!isEmpty`
- `str.length > 0`: uses `!isEmpty`
- `str.length >= 1`: uses `!isEmpty`
- Boxing of value types: value types are interned. Primitive types like `Number` are interned in more depth, for example, values under < 512 are looked up into a particular collection, `String`s are divided into collections by length and `Boolean` is simply binary.