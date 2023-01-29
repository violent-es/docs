# Built-in Objects

## global

This is a property that refers to the global package.

## Iterator.\<T>

**Extends:** Generator.\<T>

**Proxies:**

- `proxy::has`: tests if value is contained in a collection

**Methods:**

- `next():{done:Boolean, value:undefined|T}`
- `toArray():[T]`
- Array-like functional methods such as `map()` and `some()`

## INodeContainer.\<T>

Interface for markup expressions such as `<C></C>`.

**Methods:**

- `INodeContainer_add(child:T):void`

## DecoratorProperty

**Properties:**

- `name:String`
- `type:Class`
- `writable:Boolean`