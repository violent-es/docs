# Future Features

## Alias

The following `use` definition should not be needed at all, because the user can already alias types and namespaces with the context words `type` and `namespace`. The following `use` should only be useful for aliasing functions and variables.

Inclusively, the `namespace` definition can also alias a package.

```
// form 1 (re-exports B)
public use q.f.B;

// form 2 (re-exports B as A)
public use A = q.f.B;
```