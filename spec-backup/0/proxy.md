# Proxy

```
class C {
    // the following proxy definitions have no 'this' literal available

    proxy function convertImplicit(a:T):C? {
        // conversion
    }

    proxy function convertExplicit(a:T):C? {
        // conversion
    }

    // +o;
    proxy function positive(a)
        ...;

    // -o;
    proxy function negate(a)
        ...;

    // ~o;
    proxy function bitNot(a)
        ...;

    // a === b;
    proxy function equals(a, b)
        ...;

    // a !== b;
    proxy function notEquals(a, b)
        ...;

    // a < b;
    proxy function lt(a, b)
        ...;

    // a > b;
    proxy function gt(a, b)
        ...;

    // a <= b;
    proxy function le(a, b)
        ...;

    // a >= b;
    proxy function ge(a, b)
        ...;

    // a + b;
    proxy function add(a, b)
        ...;

    // a - b;
    proxy function subtract(a, b)
        ...;

    // a * b;
    proxy function multiply(a, b)
        ...;

    // a / b;
    proxy function divide(a, b)
        ...;

    // a % b;
    proxy function remainder(a, b)
        ...;

    // a ** b;
    proxy function pow(a, b)
        ...;

    // a & b;
    proxy function bitAnd(a, b)
        ...;

    // a ^ b;
    proxy function bitXor(a, b)
        ...;

    // a | b;
    proxy function bitOr(a, b)
        ...;

    // a << b;
    proxy function leftShift(a, b)
        ...;

    // a >> b;
    proxy function rightShift(a, b)
        ...;

    // a >>> b;
    proxy function unsignedRightShift(a, b)
        ...;

    // the following proxy definitions have 'this' literal available

    // o[i];
    proxy function getIndex(i)
        ...;

    // o[i] = v;
    proxy function setIndex(i, v) {
        ...
    }

    // delete o[i];
    proxy function deleteIndex(i):Boolean
        ...;

    // v in o;
    proxy function has(v):Boolean
        ...;

    // for..in
    proxy function iterateKeys():Generator.<K> {
        // yield
    }

    // for each
    proxy function iterateValues():Generator.<V> {
        // yield
    }
}
```