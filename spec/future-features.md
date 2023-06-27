# Future Features

## Alias

The following `use alias` definition should not be needed at all, because the user can already alias types and namespaces with the context words `type` and `namespace`. The following `use alias` should only be useful for aliasing functions and variables.

Inclusively, the `namespace` definition can also alias a package.

```
// form 1 (re-exports B)
public use alias q.f.B;

// form 2 (re-exports B as A)
public use alias A = q.f.B;
```

It is also worthy noting lexical aliases are already possible with `import`.

## Observable Object

Based on an ECMAScript proposal for Observable.

## Type Inference for Override Signatures

Libraries are usually loaded and resolved before an actual project, therefore it can be useful to override a method whose signature has already been resolved without specifying its types.

```
class C extends CanvasLayer {
    override function process(delta) {
    }
}
```

## Script-Level Allows and Warnings

There is no need so far, but if needed in the future, a script can specify an allow or warn using a top string literal (like `'allow ...'`). In this case they've to be syntatically consumed before packages (including the optional semicolon).

This would use a stack too, for allowing `include`d scripts to alter it for theirselves.