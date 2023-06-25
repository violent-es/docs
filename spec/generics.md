# Generics

```
class C.<T> {
}
// T extends or implements F
class C2.<T:F> {
}
// where clauses are optional
function f.<T>(v:T):void where T is SomeBound {
}
// where clause may be repeated, or comma list can be used
function g.<T>(v:T):void where T is A, T is B {
}
```

Use one or more `where` clauses for different type parameter bounds.