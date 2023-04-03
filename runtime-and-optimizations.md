# Runtime and Optimizations

- `array.push(v);`: takes only one argument, so do not create an `Array` for rest arguments.
- `for each (var i in Number.range(0, 10) ...;`: optimize loop by skipping `Generator` instance and skipping step parameter.
- `String` is internally either original or a slice of another one. When the type is boxed, this is not the case.
- Boxing of value types: value types are interned. Primitive types like `Number` are interned in more depth, for example, values under < 512 are looked up into a particular collection, `String`s are divided into collections by length and `Boolean` is simply binary. These internation collections should preferably consist of weak references whenever possible in the host environment.
- In native host environments, for the `*` type, a `undefined` value is identified by variant 0, `null` by variant 1 and anything else is an actual `Object` reference address.