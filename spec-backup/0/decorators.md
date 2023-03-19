# Decorators

A decorator is a function that either returns `void` or returns another function that returns `void`, applied to either a type, property or method.

`[D(x = 10)]` is equivalent to `[D({x: 10})]`.

## Decorators applied to types

```
function MyTypeDecorator(type:Class):void {
}

[MyTypeDecorator]
class C {
}
```

## Decorators applied to properties

```
function MyFieldDecorator(o:C, {name}:DecoratorProperty):void {
    trace(name);
}

class C {
    [MyFieldDecorator]
    public var x:Number;
}
```

## Decorators applied to methods

```
function MyMethodDecorator(o:C, name:String):void {
    trace(name);
}

class C {
    [MyMethodDecorator]
    public function f():void {
    }
}
```

## Reserved

The following decorators are reserved, but can still be used if they do not directly appear as lexical references:

- When applied to a class, `[Value]` is reserved
- When applied to a class, `[DontInit]` is reserved
- When applied to an enum, `[Flags]` is reserved

## Futurely-reserved

- `[Partial]` applied to classes and enums.