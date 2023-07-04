# Package Manager

As usual, dependencies will be expressed into a configuration file.

`include`s without initial dot are reserved as they may be used in the future.

```
include 'com.library@0.1.0';
```

In that case, this _**wouldn't**_ include the library sources syntatically. That `include` would be collected and removed from the program before verification or evaluation.