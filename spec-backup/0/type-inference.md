# Type inference

## Enum

```
var e:E?;

e = 'fooConstant';
e = E.FOO_CONSTANT;

var flags:F = undefined; // empty
flags = ['flagA', 'flagB'];
flags = {flagA: true,  flagB: true};
flags = [Flags.FLAG_A, Flags.FLAG_B];
```