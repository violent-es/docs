# Type Conversions

Constant implicit:
- `undefined` to nullable type without `undefined` (results in `null`)
- `undefined` to type with `undefined` (results in `undefined`)
- `undefined` to flags enum
- `null` to type containing `null` but no `undefined`
- `null` to type containing `undefined` but no `null` (results in `undefined`)
- `null` to type containing `undefined` and `null`
- To number type with wider range

Implicit:
- User implicit
- To number type with wider range
- Non-union to compatible union
- Union to compatible union
- Union with null or undefined to compatible union with null or undefined
- From record to record with equivalent field set
- From any
- To any
- To covariant type

Explicit:
- User explicit
- To union member
- To contravariant type
- To covariant `Array`
- To contravariant `Array`
- Between numeric types
- From string to enum
- From number to enum