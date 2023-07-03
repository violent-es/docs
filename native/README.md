# Native

## Writing Basic Base Class

A native class that is not marked `final` should specify the count of bytes for its internal fields. This count of bytes:

- _doesn't_ include internal fields from supertypes and
- _doesn't_ include internal fields from subtypes.

The class would usually look like this in the Rust side:

```
#[repr(C)]
struct C1 {
    constructor: u64,
    fields: u64,
}
```

where:

- `constructor` is a property defined internally by `Object`. It's a pointer to a `Box`.
- `fields` is a pointer to `C1`'s fields (usually a `Box`).

Therefore, `C1` can be defined in VioletScript as:

```
[FFI(memorySize = 8)]
public class C1 {
}
```

since `fields` is an unsigned 64-bit integer.